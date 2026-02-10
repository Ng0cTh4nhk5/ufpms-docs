# Module 2: Approval Workflow - Medium-Level Use Cases

> **Module**: 2 - Approval Workflow  
> **High-Level UC**: [UC-HL-002](../High_Level/uc_hl_02_approval_workflow.md)

---

## Researcher Actions

### UC-M2-001: Submit for Review
**ID**: UC-M2-001 | **Priority**: 🔴 P0 | **Actor**: Researcher  
**Related**: US-RES-010, FR-APR-001

**Goal**: Submit publication for faculty review  
**Preconditions**: Publication status = DRAFT, all required fields filled  
**Main Flow**:  
1. Researcher clicks "Submit for Review"
2. System validates required fields (Title, Authors, Year, PDF)
3. System changes status: DRAFT → SUBMITTED
4. System sends emaillto Faculty Reviewer
5. System logs audit trail

**Postconditions**: Status = SUBMITTED, notification sent  
**Business Rules**: BR-APR-001, BR-APR-004

---

### UC-M2-002: Track Review Status
**ID**: UC-M2-002 | **Priority**: 🔴 P0 | **Actor**: Researcher  
**Related**: US-RES-011, FR-APR-002

**Goal**: View current review status and history  
**Main Flow**:
1. Researcher views publication details
2. System displays status timeline
3. System shows current status highlighted
4. System shows reviewer comments (if any)
5. System shows date of each transition

**Business Rules**: Show complete audit trail

---

### UC-M2-003: Revise Publication
**ID**: UC-M2-003 | **Priority**: 🔴 P0 | **Actor**: Researcher  
**Related**: US-RES-012, FR-APR-003

**Goal**: Revise and resubmit after reviewer feedback  
**Preconditions**: Status = REVISION_REQUIRED  
**Main Flow**:
1. Researcher views reviewer comments
2. Researcher clicks "Edit"
3. Researcher makes changes
4. Researcher clicks "Resubmit"
5. System changes status: REVISION_REQUIRED → SUBMITTED
6. System sends email to Faculty Reviewer

**Business Rules**: BR-APR-001

---

### UC-M2-004: Withdraw Submission
**ID**: UC-M2-004 | **Priority**: 🟡 P1 | **Actor**: Researcher  
**Related**: US-RES-013, FR-APR-019

**Goal**: Withdraw submission before approval  
**Preconditions**: Status = SUBMITTED or FACULTY_REVIEWING  
**Main Flow**:
1. Researcher clicks "Withdraw"
2. System confirms action
3. System changes status back to DRAFT
4. System sends email to reviewer (if reviewing)

---

## Faculty Reviewer Actions

### UC-M2-005: Faculty Review - Approve
**ID**: UC-M2-005 | **Priority**: 🔴 P0 | **Actor**: Faculty Reviewer  
**Related**: US-FCR-002, FR-APR-006

**Goal**: Approve publication at faculty level  
**Preconditions**: Status = FACULTY_REVIEWING, user is faculty reviewer  
**Main Flow**:
1. Reviewer views publication
2. Reviewer clicks "Approve"
3. Reviewer adds optional comment
4. System changes status: FACULTY_REVIEWING → FACULTY_APPROVED
5. System sends email to:
   - Researcher: "Approved by Faculty"
   - University Reviewer: "Pending review"
6. System logs audit trail

**Postconditions**: Status = FACULTY_APPROVED  
**Business Rules**: BR-APR-001, BR-APR-002, BR-APR-004

---

### UC-M2-006: Faculty Review - Request Revision
**ID**: UC-M2-006 | **Priority**: 🔴 P0 | **Actor**: Faculty Reviewer  
**Related**: US-FCR-003, FR-APR-007

**Goal**: Request revisions from researcher  
**Main Flow**:
1. Reviewer clicks "Request Revision"
2. Reviewer enters comment (min 10 chars, required)
3. System changes status: FACULTY_REVIEWING → REVISION_REQUIRED
4. System sends email to Researcher with comment
5. System logs audit trail

**Business Rules**: BR-APR-005 (comment required)

---

### UC-M2-007: Faculty Review - Reject
**ID**: UC-M2-007 | **Priority**: 🔴 P0 | **Actor**: Faculty Reviewer  
**Related**: US-FCR-004, FR-APR-008

**Goal**: Reject publication (final decision)  
**Main Flow**:
1. Reviewer clicks "Reject"
2. Reviewer enters reason (min 20 chars, required)
3. System changes status: FACULTY_REVIEWING → FACULTY_REJECTED
4. System sends email to Researcher
5. System logs audit trail

**Postconditions**: Status = FACULTY_REJECTED (cannot resubmit)  
**Business Rules**: BR-APR-003 (finality)

---

### UC-M2-012: Bulk Approve (Faculty)
**ID**: UC-M2-012 | **Priority**: 🟡 P1 | **Actor**: Faculty Reviewer  
**Related**: US-FCR-007, FR-APR-009

**Goal**: Approve multiple publications at once  
**Main Flow**:
1. Reviewer selects multiple publications (checkboxes)
2. Reviewer clicks "Approve Selected"
3. System confirms action
4. System approves all selected
5. System sends individual emails
6. System sends summary email to University Reviewer

---

## University Reviewer Actions

### UC-M2-008: University Review - Approve & Publish
**ID**: UC-M2-008 | **Priority**: 🔴 P0 | **Actor**: University Reviewer  
**Related**: US-UNR-003, FR-APR-012

**Goal**: Final approval and publish to public  
**Preconditions**: Status = UNIVERSITY_REVIEWING  
**Main Flow**:
1. Reviewer views publication and faculty comments
2. Reviewer clicks "Approve & Publish"
3. System changes status: UNIVERSITY_REVIEWING → PUBLISHED
4. System makes publication visible in public search
5. System displays on researcher's public profile
6. System sends email to Researcher: "Published!"
7. System logs audit trail

**Postconditions**: Status = PUBLISHED, visible publicly  
**Business Rules**: BR-APR-002, BR-SEA-001

---

### UC-M2-009: University Review - Reject
**ID**: UC-M2-009 | **Priority**: 🔴 P0 | **Actor**: University Reviewer  
**Related**: US-UNR-004, FR-APR-013

**Goal**: Reject at university level  
**Main Flow**:
1. Reviewer clicks "Reject"
2. Reviewer enters reason (required)
3. System changes status: UNIVERSITY_REVIEWING → UNIVERSITY_REJECTED
4. System sends emails to Researcher and Faculty Reviewer

**Postconditions**: Status = UNIVERSITY_REJECTED (final)  
**Business Rules**: BR-APR-003

---

### UC-M2-013: Bulk Approve (University)
**ID**: UC-M2-013 | **Priority**: 🟡 P1 | **Actor**: University Reviewer  
**Goal**: Approve and publish multiple publications

**Main Flow**: Similar to UC-M2-012 but results in PUBLISHED status

---

### UC-M2-014: Reassign Reviewer
**ID**: UC-M2-014 | **Priority**: 🟡 P1 | **Actor**: SuperAdmin  
**Related**: FR-APR-018

**Goal**: Change assigned reviewer  
**Main Flow**:
1. Admin views publication
2. Admin clicks "Reassign"
3. Admin selects new reviewer
4. System sends notification to new reviewer

---

## System Actions

### UC-M2-010: View Review History
**ID**: UC-M2-010 | **Priority**: 🔴 P0 | **Actor**: All reviewers  
**Related**: US-FCR-005, US-UNR-005, FR-APR-015

**Goal**: View complete audit trail  
**Main Flow**:
1. User views publication details
2. User clicks "Review History" tab
3. System displays all state transitions:
   - Timestamp
   - From/To status
   - Reviewer name and role
   - Comments
4. Sorted: Newest first

---

### UC-M2-011: Send Email Notifications
**ID**: UC-M2-011 | **Priority**: 🔴 P0 | **Actor**: System  
**Related**: US-FCR-006, US-UNR-006, FR-APR-016

**Goal**: Send automated email on status changes  
**Main Flow**:
1. Publication status changes
2. System determines recipients based on new status
3. System generates email content
4. System sends email via SMTP
5. System logs email sent event

**Email Templates**:
- SUBMITTED → Faculty Reviewer
- REVISION_REQUIRED → Researcher
- FACULTY_APPROVED → Researcher + University Reviewer
- PUBLISHED → Researcher

**Business Rules**: BR-APR-004 (must include direct link)

---

### UC-M2-015: SLA Monitoring
**ID**: UC-M2-015 | **Priority**: 🟢 P2 | **Actor**: System/Reviewers  
**Related**: US-FCR-009, FR-APR-020

**Goal**: Track and highlight overdue reviews  
**Main Flow**:
1. System calculates duration in current status
2. If > 7 days: Highlight as overdue
3. Dashboard shows:
   - Publications over SLA
   - Average review time
   - % within SLA

**Business Rules**: BR-APR-006 (SLA targets)

---

**Tài liệu liên quan**:
- [High-Level UC-HL-002](../High_Level/uc_hl_02_approval_workflow.md)
- [User Stories - Researcher, Reviewers](../../04_User_Stories/By_Role/)
- [Requirements - Approval Workflow](../../03_Requirements/Functional/module_approval_workflow.md)
