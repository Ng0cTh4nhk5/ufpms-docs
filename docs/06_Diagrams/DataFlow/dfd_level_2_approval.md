# DFD Level 2 - Approval Workflow Detail

> 📊 **Level**: 2 (Detailed Process Decomposition)  
> 🎯 **Scope**: Approval Workflow module decomposition  
> 📅 **Created**: 11/02/2026

---

## 📊 Data Flow Diagram Level 2

```mermaid
flowchart TD
    subgraph External["External Entities"]
        RES[Researcher]
        FCR[Faculty Reviewer]
        UNR[University Reviewer]
    end
    
    subgraph Level_2_Processes["2.0 Approval Workflow - Detailed Processes"]
        P21["2.1<br/>Validate<br/>Submission"]
        P22["2.2<br/>Assign<br/>Faculty Reviewer"]
        P23["2.3<br/>Faculty<br/>Review"]
        P24["2.4<br/>University<br/>Review"]
        P25["2.5<br/>Update<br/>Publication Status"]
        P26["2.6<br/>Send<br/>Notifications"]
        P27["2.7<br/>Log<br/>History"]
    end
    
    subgraph DataStores["Data Stores"]
        D1[(D1: Publications)]
        D2[(D2: Users)]
        D3[(D3: Review History)]
        D4[(D4: Review Comments)]
    end
    
    %% External to Process flows
    RES -->|Submit request| P21
    FCR -->|Review decision| P23
    UNR -->|Approval decision| P24
    
    %% Process to External flows
    P26 -->|Submission received email| RES
    P26 -->|Review assignment email| FCR
    P26 -->|Status update email| RES
    P26 -->|Final approval email| RES
    
    %% Process to Data Store flows
    P21 <-->|Read publication| D1
    P22 -->|Read reviewers by faculty| D2
    P23 <-->|Read publication| D1
    P24 <-->|Read publication| D1
    P25 -->|Write status update| D1
    P26 <-->|Read user emails| D2
    P27 -->|Write history record| D3
    P23 -->|Write comments| D4
    P24 -->|Write comments| D4
    
    %% Inter-process flows
    P21 -->|Valid submission| P22
    P22 -->|Assigned reviewer| P23
    P23 -->|Faculty approved| P24
    P23 -->|Revision required| P25
    P23 -->|Rejected| P25
    P24 -->|University approved| P25
    P24 -->|Send back| P22
    P25 -->|Status changed| P26
    P25 -->|Status changed| P27
    
    style P21 fill:#ffccbc
    style P22 fill:#ffab91
    style P23 fill:#ff8a65
    style P24 fill:#ff7043
    style P25 fill:#ff6b9d
    style P26 fill:#ffcdd2
    style P27 fill:#f8bbd0
```

---

## 📋 Detailed Process Specifications

### 2.1 Validate Submission

**Input**:
- Submit request (from Researcher)
- Publication data (from D1)

**Process**:
1. Check publication status = DRAFT
2. Check ownership (submitter = owner)
3. Validate required fields:
   - Title filled
   - At least 1 author
   - PDF uploaded
4. Check duplicate DOI (if provided)

**Output**:
- Valid submission → to 2.2
- Invalid submission → error message to Researcher

**Data Store Access**:
- READ: D1 (Publications)

---

### 2.2 Assign Faculty Reviewer

**Input**:
- Valid submission (from 2.1)

**Process**:
1. Get researcher's faculty
2. Query active faculty reviewers
3. Select reviewer (round-robin P2, manual P0)
4. Update publication with reviewer assignment

**Output**:
- Assigned reviewer info → to 2.3
- Reviewer notification trigger → to 2.6

**Data Store Access**:
- READ: D2 (Users - get reviewers)
- WRITE: D1 (Publications - assign reviewer)

**Business Rule**:
- Reviewer must be from same faculty
- Reviewer cannot review own publications

---

### 2.3 Faculty Review

**Input**:
- Review decision (from Faculty Reviewer)
- Publication data (from D1)

**Process**:
1. Validate reviewer authorization
2. Process decision:
   - **Approve**: Set status = FACULTY_APPROVED → to 2.4
   - **Request Revision**: Set status = REVISION_REQUIRED → to 2.5
   - **Reject**: Set status = REJECTED → to 2.5
3. Save comments (if provided)

**Output**:
- Approved → to 2.4 (University Review)
- Revision/Rejected → to 2.5 (Update Status)

**Data Store Access**:
- READ: D1 (Publications)
- WRITE: D4 (Review Comments)

---

### 2.4 University Review

**Input**:
- Approval decision (from University Reviewer)
- Publication data (from D1)

**Process**:
1. Validate reviewer authorization (University Reviewer role)
2. Process decision:
   - **Approve**: Set status = PUBLISHED → to 2.5
   - **Send Back**: Set status = FACULTY_REVIEWING → to 2.2

**Output**:
- Approved/Sent Back → to 2.5 (Update Status)

**Data Store Access**:
- READ: D1 (Publications)
- WRITE: D4 (Review Comments)

**Business Rule**:
- Only University Reviewers can publish
- Published publications cannot be edited by researcher

---

### 2.5 Update Publication Status

**Input**:
- Status change (from 2.3 or 2.4)
- New status value
- Old status value

**Process**:
1. Update publications table (set status, timestamps)
2. If PUBLISHED: set published_at = NOW()

**Output**:
- Status updated → trigger to 2.6, 2.7

**Data Store Access**:
- WRITE: D1 (Publications)

**Transaction**: Must be atomic

---

### 2.6 Send Notifications

**Input**:
- Status change event (from 2.5)
- User data (from D2)

**Process**:
1. Determine recipients based on event:
   - SUBMITTED → Faculty reviewers
   - FACULTY_APPROVED → Researcher (owner)
   - REVISION_REQUIRED → Researcher
   - REJECTED → Researcher
   - PUBLISHED → Researcher + co-authors
2. Compose email from template
3. Send via Email Server (external)

**Output**:
- Emails sent to recipients

**Data Store Access**:
- READ: D2 (Users - get emails)

**Async**: Email sending should be asynchronous (queue)

---

### 2.7 Log History

**Input**:
- Status change event (from 2.5)
- Actor (reviewer/researcher)
- Comments (if any)

**Process**:
1. Create history record:
   - from_status
   - to_status
   - actor_id
   - action
   - timestamp

**Output**:
- History record saved

**Data Store Access**:
- WRITE: D3 (Review History)

**Audit**: Immutable records for compliance

---

## 🔄 Workflow State Transitions

```mermaid
stateDiagram-v2
    [*] --> DRAFT: Create
    DRAFT --> SUBMITTED: 2.1 Validate
    SUBMITTED --> FACULTY_REVIEWING: 2.2 Assign
    
    FACULTY_REVIEWING --> FACULTY_APPROVED: 2.3 Approve
    FACULTY_REVIEWING --> REVISION_REQUIRED: 2.3 Request Revision
    FACULTY_REVIEWING --> REJECTED: 2.3 Reject
    
    REVISION_REQUIRED --> DRAFT: Researcher edits
    
    FACULTY_APPROVED --> UNIVERSITY_REVIEWING: 2.4 Auto-transition
    
    UNIVERSITY_REVIEWING --> PUBLISHED: 2.4 Approve
    UNIVERSITY_REVIEWING --> FACULTY_REVIEWING: 2.4 Send Back
    
    PUBLISHED --> [*]
    REJECTED --> [*]
```

---

## 📊 Data Store Details

### D1: Publications
**Accessed by**: 2.1, 2.2, 2.3, 2.4, 2.5  
**Operations**: READ, WRITE (status updates)

### D2: Users
**Accessed by**: 2.2, 2.6  
**Operations**: READ only (get reviewers, get emails)

### D3: Review History
**Accessed by**: 2.7  
**Operations**: WRITE only (append-only audit log)

### D4: Review Comments
**Accessed by**: 2.3, 2.4  
**Operations**: WRITE (insert comments)

---

## ⏱️ Process Timing

| Process | Avg Duration | Type |
|---------|-------------|------|
| 2.1 Validate | < 1 second | Synchronous |
| 2.2 Assign | < 2 seconds | Synchronous |
| 2.3 Faculty Review | 3-7 days | Human decision |
| 2.4 University Review | 3-7 days | Human decision |
| 2.5 Update Status | < 1 second | Synchronous |
| 2.6 Notifications | 2-5 seconds | Asynchronous |
| 2.7 Log History | < 1 second | Synchronous |

**Total SLA**: 6-14 days (DRAFT → PUBLISHED)

---

**Related**: act_approval_workflow.md, seq_faculty_review.md, seq_university_approval.md  
**Created**: 11/02/2026
