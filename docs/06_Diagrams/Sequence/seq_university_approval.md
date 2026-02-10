# Sequence Diagram: University Final Approval

> 📊 **Diagram ID**: SEQ-04  
> 🎯 **Use Case**: UC-D2-11 - University Final Approval  
> 👤 **Actor**: University Reviewer  
> ⚙️ **Result**: PUBLISHED or sent back to Faculty

---

## 📊 Sequence Diagram

```mermaid
sequenceDiagram
    actor Reviewer as 👨‍💼 University Reviewer
    participant UI as 🖥️ UI
    participant API as 🔌 API
    participant Service as ⚙️ WorkflowService
    participant Repo as 💾 Repository
    participant DB as 🗄️ Database
    participant Notif as 📧 Notification
    
    %% Get pending
    Reviewer->>UI: View university reviews
    UI->>API: GET /api/reviews/university
    API->>Service: getUniversityPendingReviews()
    Service->>Repo: findByStatus("UNIVERSITY_REVIEWING")
    Repo->>DB: SELECT * WHERE status = 'UNIVERSITY_REVIEWING'
    DB-->>Repo: List
    Repo-->>Service: Publications[]
    Service-->>API: Data
    API-->>UI: Pending reviews
    UI-->>Reviewer: Display list
    
    %% View details
    Reviewer->>UI: Click publication
    UI->>API: GET /api/publications/{id}
    API->>Repo: findWithHistory(id)
    Repo->>DB: SELECT with review_history
    DB-->>Repo: Full data + faculty comments
    Repo-->>API: Publication
    API-->>UI: Details
    UI-->>Reviewer: Show publication +<br/>faculty review comments
    
    alt Final Approve → PUBLISH
        Reviewer->>UI: Click "Publish"
        UI->>API: POST /api/reviews/{id}/publish
        activate API
        API->>Service: publishPublication(pubId, reviewerId)
        activate Service
        
        Note over Service,DB: START TRANSACTION
        
        %% Update status
        Service->>Repo: updateStatus(pubId, "PUBLISHED")
        activate Repo
        Repo->>DB: UPDATE publications<br/>SET status = 'PUBLISHED',<br/>published_at = NOW()
        deactivate Repo
        
        %% Log history
        Service->>Repo: createReviewHistory(entry)
        Repo->>DB: INSERT INTO review_history<br/>(from: UNIVERSITY_REVIEWING,<br/>to: PUBLISHED,<br/>actor: reviewerId)
        
        %% Audit log
        Service->>Repo: logAudit(...)
        Repo->>DB: INSERT INTO audit_logs
        
        Note over Service,DB: COMMIT
        
        %% Notifications
        Service->>Notif: notifyPublished(publication)
        activate Notif
        
        Note over Notif: Notify:<br/>- Researcher (owner)<br/>- All co-authors<br/>- Faculty reviewer
        
        loop For each recipient
            Notif->>Notif: Send email
        end
        
        deactivate Notif
        
        Service-->>API: Success
        deactivate Service
        API-->>UI: 200 OK + Published publication
        deactivate API
        UI-->>Reviewer: "Published successfully!"<br/>+ Link to public view
        
    else Send Back to Faculty
        Reviewer->>UI: Click "Send Back to Faculty"
        UI->>UI: Require reason
        Reviewer->>UI: Enter reason
        
        UI->>API: POST /api/reviews/{id}/send-back
        activate API
        API->>Service: sendBackToFaculty(pubId, reviewerId, reason)
        activate Service
        
        Note over Service,DB: START TRANSACTION
        
        Service->>Repo: updateStatus(pubId, "FACULTY_REVIEWING")
        Repo->>DB: UPDATE publications<br/>SET status = 'FACULTY_REVIEWING'
        
        Service->>Repo: saveComments(pubId, reviewerId, reason)
        Repo->>DB: INSERT INTO review_comments
        
        Service->>Repo: createReviewHistory(entry)
        Repo->>DB: INSERT INTO review_history
        
        Note over Service,DB: COMMIT
        
        Service->>Notif: notifySentBack(publication, reason)
        activate Notif
        Notif->>Notif: Notify faculty reviewer
        deactivate Notif
        
        Service-->>API: Success
        deactivate Service
        API-->>UI: 200 OK
        deactivate API
        UI-->>Reviewer: "Sent back to faculty"
    end
```

---

## 📋 Two Actions

### 1. Final Approve → Publish ✅
**Effect**:
- Status: `UNIVERSITY_REVIEWING` → `PUBLISHED`
- `published_at` timestamp set
- Publication becomes **publicly visible**

**Notifications**:
1. Researcher (owner)
2. All co-authors
3. Faculty reviewer (FYI)

**Email Content**:
```
Subject: Your publication has been published!

Dear {researcher_name},

Congratulations! Your publication has been approved and published:

Title: {title}
Published: {timestamp}

View public page: {public_url}

Best regards,
UFPMS
```

---

### 2. Send Back to Faculty 🔄
**Effect**:
- Status: `UNIVERSITY_REVIEWING` → `FACULTY_REVIEWING`
- Faculty reviewer needs to re-review

**Use Cases**:
- University reviewer disagrees with faculty decision
- Found issues not caught by faculty
- Needs more information

**Reason required**: Why sending back

---

## 🗄️ Database Changes

### Publish
```sql
UPDATE publications 
SET status = 'PUBLISHED',
    published_at = NOW(),
    updated_at = NOW()
WHERE id = ? AND status = 'UNIVERSITY_REVIEWING';

INSERT INTO review_history (
    publication_id, from_status, to_status,
    actor_id, action, timestamp
) VALUES (
    ?, 'UNIVERSITY_REVIEWING', 'PUBLISHED',
    ?, 'FINAL_APPROVE', NOW()
);
```

### Send Back
```sql
UPDATE publications 
SET status = 'FACULTY_REVIEWING',
    updated_at = NOW()
WHERE id = ?;

INSERT INTO review_comments (
    publication_id, reviewer_id, 
    comment_type, comment_text, timestamp
) VALUES (
    ?, ?, 'SENT_BACK_REASON', ?, NOW()
);
```

---

## 🔒 Business Rules

1. **Only University Reviewers** can publish
2. After PUBLISHED:
   - Researcher **cannot edit** (only SuperAdmin)
   - Researcher **cannot delete** (only SuperAdmin)
   - Publication visible to **public**
3. Published publication counts toward:
   - Researcher statistics
   - Faculty/University reports
   - Public search results

---

## 📈 Post-Publication Effects

### Visibility
- Appears in public search
- Visible on researcher's profile
- Included in faculty/university reports

### Statistics Update
- Researcher publication count +1
- Faculty publication count +1
- University publication count +1

### Analytics (P2)
- Citation tracking enabled
- Download tracking enabled

---

**Related**: FR-APR-013, FR-APR-014, US-UNR-004, US-UNR-005  
**Created**: 10/02/2026
