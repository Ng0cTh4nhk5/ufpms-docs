# Sequence Diagram: Faculty Review Process

> 📊 **Diagram ID**: SEQ-03  
> 🎯 **Use Case**: UC-D2-05 - Faculty Review  
> 👤 **Actor**: Faculty Reviewer  
> ⚙️ **Key**: Review, Approve/Reject/Request Revision

---

## 📊 Sequence Diagram

```mermaid
sequenceDiagram
    actor Reviewer as 👨‍💼 Faculty Reviewer
    participant UI as 🖥️ React UI
    participant API as 🔌 WorkflowController
    participant Service as ⚙️ WorkflowService
    participant Repo as 💾 Repository
    participant DB as 🗄️ Database
    participant Notif as 📧 NotificationService
    
    %% View submissions
    Reviewer->>UI: Navigate to "My Reviews"
    UI->>API: GET /api/reviews/pending
    API->>Service: getPendingReviews(reviewerId)
    Service->>Repo: findByFacultyAndStatus(facultyId, "FACULTY_REVIEWING")
    Repo->>DB: SELECT * WHERE faculty_id = ?<br/>AND status = 'FACULTY_REVIEWING'
    DB-->>Repo: Publications list
    Repo-->>Service: Publications[]
    Service-->>API: Publications
    API-->>UI: List of pending reviews
    UI-->>Reviewer: Display list
    
    %% View details
    Reviewer->>UI: Click publication
    UI->>API: GET /api/publications/{id}
    API->>Repo: findById(id)
    Repo->>DB: SELECT with authors, PDF
    DB-->>Repo: Full publication data
    Repo-->>API: Publication
    API-->>UI: Publication details
    UI-->>Reviewer: Show details + PDF viewer
    
    %% Add comments
    Reviewer->>UI: Type review comments
    Reviewer->>UI: Select action: Approve/Revision/Reject
    
    alt Action: Approve
        Reviewer->>UI: Click "Approve"
        UI->>API: POST /api/reviews/{id}/approve
        activate API
        
        API->>Service: approveAtFaculty(pubId, reviewerId, comments)
        activate Service
        
        Note over Service,DB: START TRANSACTION
        
        %% Update status
        Service->>Repo: updateStatus(pubId, "FACULTY_APPROVED")
        Repo->>DB: UPDATE publications<br/>SET status = 'FACULTY_APPROVED'
        
        %% Auto transition to university review
        Service->>Repo: updateStatus(pubId, "UNIVERSITY_REVIEWING")
        Repo->>DB: UPDATE publications<br/>SET status = 'UNIVERSITY_REVIEWING'
        
        %% Log review
        Service->>Repo: createReviewHistory(entry)
        Repo->>DB: INSERT INTO review_history
        
        %% Save comments
        alt Comments provided
            Service->>Repo: saveComments(pubId, reviewerId, comments)
            Repo->>DB: INSERT INTO review_comments
        end
        
        Note over Service,DB: COMMIT
        
        %% Notify
        Service->>Notif: notifyFacultyApproval(publication)
        activate Notif
        Notif->>Notif: Notify researcher (approved)
        Notif->>Notif: Notify university reviewers (new task)
        deactivate Notif
        
        Service-->>API: Success
        deactivate Service
        API-->>UI: 200 OK
        deactivate API
        UI-->>Reviewer: "Approved successfully"
        
    else Action: Request Revision
        Reviewer->>UI: Click "Request Revision"
        UI->>UI: Require comments
        Reviewer->>UI: Enter revision reasons
        
        UI->>API: POST /api/reviews/{id}/request-revision
        activate API
        API->>Service: requestRevision(pubId, reviewerId, comments)
        activate Service
        
        Note over Service,DB: START TRANSACTION
        
        Service->>Repo: updateStatus(pubId, "REVISION_REQUIRED")
        Repo->>DB: UPDATE publications<br/>SET status = 'REVISION_REQUIRED'
        
        Service->>Repo: saveComments(pubId, reviewerId, comments)
        Repo->>DB: INSERT INTO review_comments
        
        Service->>Repo: createReviewHistory(entry)
        Repo->>DB: INSERT INTO review_history
        
        Note over Service,DB: COMMIT
        
        Service->>Notif: notifyRevisionRequired(publication, comments)
        activate Notif
        Notif->>Notif: Send email to researcher with comments
        deactivate Notif
        
        Service-->>API: Success
        deactivate Service
        API-->>UI: 200 OK
        deactivate API
        UI-->>Reviewer: "Revision requested"
        
    else Action: Reject
        Reviewer->>UI: Click "Reject"
        UI->>UI: Require rejection reason
        Reviewer->>UI: Enter reason
        
        UI->>API: POST /api/reviews/{id}/reject
        activate API
        API->>Service: rejectPublication(pubId, reviewerId, reason)
        activate Service
        
        Note over Service,DB: START TRANSACTION
        
        Service->>Repo: updateStatus(pubId, "REJECTED")
        Repo->>DB: UPDATE publications<br/>SET status = 'REJECTED'
        
        Service->>Repo: saveComments(pubId, reviewerId, reason)
        Repo->>DB: INSERT INTO review_comments
        
        Service->>Repo: createReviewHistory(entry)
        Repo->>DB: INSERT INTO review_history
        
        Note over Service,DB: COMMIT
        
        Service->>Notif: notifyRejection(publication, reason)
        activate Notif
        Notif->>Notif: Send email to researcher
        deactivate Notif
        
        Service-->>API: Success
        deactivate Service
        API-->>UI: 200 OK
        deactivate API
        UI-->>Reviewer: "Publication rejected"
    end
```

---

## 📋 Three Actions

### 1. Approve ✅
- Status: `FACULTY_REVIEWING` → `FACULTY_APPROVED` → `UNIVERSITY_REVIEWING`
- Notification: Researcher (approved) + University Reviewers (new task)
- Comments optional

### 2. Request Revision 📝
- Status: `FACULTY_REVIEWING` → `REVISION_REQUIRED`
- Researcher can re-edit → resubmit
- Comments **required**

### 3. Reject ❌
- Status: `FACULTY_REVIEWING` → `REJECTED`
- Final rejection (cannot resubmit without SuperAdmin)
- Reason **required**

---

## 🗄️ Database Changes

### Approve
```sql
-- Status transitions
UPDATE publications SET status = 'FACULTY_APPROVED' WHERE id = ?;
UPDATE publications SET status = 'UNIVERSITY_REVIEWING' WHERE id = ?;

-- History
INSERT INTO review_history (publication_id, from_status, to_status, actor_id, action, comments)
VALUES (?, 'FACULTY_REVIEWING', 'UNIVERSITY_REVIEWING', ?, 'APPROVE', ?);
```

### Request Revision
```sql
UPDATE publications SET status = 'REVISION_REQUIRED' WHERE id = ?;

INSERT INTO review_comments (publication_id, reviewer_id, comment_type, comment_text)
VALUES (?, ?, 'REVISION_REQUEST', ?);

INSERT INTO review_history ...
```

### Reject
```sql
UPDATE publications SET status = 'REJECTED' WHERE id = ?;

INSERT INTO review_comments (publication_id, reviewer_id, comment_type, comment_text)
VALUES (?, ?, 'REJECTION_REASON', ?);

INSERT INTO review_history ...
```

---

**Related**: FR-APR-005 to APR-009, US-FCR-002 to FCR-005  
**Created**: 10/02/2026
