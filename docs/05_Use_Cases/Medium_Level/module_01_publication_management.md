# Module 1: Publication Management - Medium-Level Use Cases

> **Module**: 1 - Publication Management  
> **High-Level UC**: [UC-HL-001](../High_Level/uc_hl_01_manage_publications.md)

---

## UC-M1-001: Create Publication

**ID**: UC-M1-001  
**Priority**: 🔴 P0  
**Actor(s)**: Researcher  
**Related User Stories**: US-RES-001  
**Related FR**: FR-PUB-001

### Goal
Researcher creates a new publication entry with required metadata.

### Preconditions
- Researcher is logged in
- Database is accessible

### Main Flow
1. Researcher clicks "Add New Publication"
2. System displays form with fields:
   - Required: Title, Authors, Year, Journal Type
   - Optional: DOI, ISSN, Abstract, Keywords, PDF
3. Researcher enters information
4. System validates input (real-time)
5. Researcher clicks "Save"
6. System sets status = DRAFT
7. System saves to database
8. System shows "Publication created successfully"

### Postconditions
**Success**: Publication exists with status DRAFT, researcher is owner  
**Failure**: No data saved, error message displayed

### Business Rules
- BR-PUB-001: Status defaults to DRAFT
- BR-PUB-004: Year validation: 1900 ≤ year ≤ current + 1
- BR-PUB-005: Created_by = current user

---

## UC-M1-002: Edit Publication

**ID**: UC-M1-002  
**Priority**: 🔴 P0  
**Actor(s)**: Researcher  
**Related User Stories**: US-RES-003  
**Related FR**: FR-PUB-004

### Goal
Researcher edits an existing publication.

### Preconditions
- Publication status = DRAFT OR REVISION_REQUIRED
- User is the owner (corresponding author)

### Main Flow
1. Researcher selects publication from list
2. Researcher clicks "Edit"
3. System displays form pre-filled with current data
4. Researcher modifies fields
5. Researcher clicks "Save"
6. System validates changes
7. System updates database
8. System logs audit trail (who, when, what changed)
9. System shows "Changes saved"

### Postconditions
**Success**: Publication updated, audit log created  
**Failure**: No changes, error shown

### Business Rules
- BR-PUB-002: Only edit if DRAFT or REVISION_REQUIRED
- BR-PUB-001: Only owner can edit

---

## UC-M1-003: Delete Publication

**ID**: UC-M1-003  
**Priority**: 🔴 P0  
**Actor(s)**: Researcher  
**Related User Stories**: US-RES-004  
**Related FR**: FR-PUB-005

### Goal
Researcher deletes a draft publication.

### Preconditions
- Publication status = DRAFT
- User is the owner

### Main Flow
1. Researcher selects publication
2. Researcher clicks "Delete"
3. System shows confirmation: "Are you sure?"
4. Researcher confirms
5. System soft deletes (sets deleted_at timestamp)
6. System removes PDF file from storage
7. System redirects to publication list

### Postconditions
**Success**: Publication soft-deleted, PDF removed  
**Failure**: No changes

### Business Rules
- BR-PUB-002: Can only delete if status = DRAFT
- BR-PUB-003: PDF file must be removed from storage

---

## UC-M1-004: View Publication List

**ID**: UC-M1-004  
**Priority**: 🔴 P0  
**Actor(s)**: Researcher  
**Related User Stories**: US-RES-005  
**Related FR**: FR-PUB-006

### Goal
Researcher views all their publications filtered by status.

### Preconditions
- Researcher is logged in

### Main Flow
1. Researcher navigates to "My Publications"
2. System queries publications where:
   - created_by = current user OR user is co-author
   - deleted_at IS NULL
3. System displays list with columns:
   - Title, Status, Updated Date, Actions
4. Researcher can filter by status: All/Draft/Submitted/Approved/Rejected
5. System allows sorting: Newest first (default)

### Postconditions
**Success**: List displayed  

### Business Rules
- Show publications where user is owner OR co-author
- Default sort: Most recently updated first

---

## UC-M1-005: View Publication Details

**ID**: UC-M1-005  
**Priority**: 🔴 P0  
**Actor(s)**: Researcher, Faculty Reviewer, University Reviewer, Admin  
**Related User Stories**: US-RES-008  
**Related FR**: FR-PUB-010

### Goal
View complete details of a publication.

### Preconditions
- User has permission (owner/reviewer/admin OR publication is PUBLISHED)

### Main Flow
1. User clicks "View Details" on publication
2. System checks permissions
3. System displays:
   - All metadata
   - Current status
   - Review history (if any)
   - PDF download link (if uploaded)
   - DOI link (if available)

### Postconditions
**Success**: Details displayed

### Business Rules
- Public can view ONLY if status = PUBLISHED
- Internal users can view based on role

---

## UC-M1-006: Upload PDF File

**ID**: UC-M1-006  
**Priority**: 🔴 P0  
**Actor(s)**: Researcher  
**Related User Stories**: US-RES-002  
**Related FR**: FR-PUB-002

### Goal
Upload PDF file for a publication.

### Preconditions
- User is the owner
- Publication exists

### Main Flow
1. Researcher selects publication
2. Researcher clicks "Upload PDF"
3. Researcher selects PDF file from computer (< 10MB)
4. System validates:
   - File type = PDF
   - File size <10MB
5. System uploads file to storage
6. System saves file path to database
7. System shows thumbnail preview
8. System shows "Upload successful"

### Postconditions
**Success**: PDF stored, path saved  
**Failure**: No file saved

### Business Rules
- BR-PUB-003: PDF only, max 10MB
- File names sanitized to prevent security issues

---

## UC-M1-007: Download PDF File

**ID**: UC-M1-007  
**Priority**: 🔴 P0  
**Actor(s)**: Researcher, Reviewer, Admin, Public (if published)  
**Related User Stories**: US-RES-009  
**Related FR**: FR-PUB-011

### Goal
Download PDF file of a publication.

### Preconditions
- Publication has PDF uploaded
- User has permission

### Main Flow
1. User views publication details
2. User clicks "Download PDF"
3. System checks permissions
4. System serves file for download
5. System logs audit trail (who downloaded, when)

### Postconditions
**Success**: File downloaded, audit logged

### Business Rules
- Public can download ONLY if status = PUBLISHED
- All downloads are logged

---

## UC-M1-008: Add Co-Authors

**ID**: UC-M1-008  
**Priority**: 🟡 P1  
**Actor(s)**: Researcher  
**Related User Stories**: US-RES-006  
**Related FR**: FR-PUB-007

### Goal
Add co-authors from university to publication.

### Preconditions
- User is the owner
- Publication is DRAFT or REVISION_REQUIRED

### Main Flow
1. Researcher edits publication
2. Researcher types name in co-authors field
3. System shows autocomplete suggestions from user database
4. Researcher selects co-author
5. System adds to co-authors list
6. Researcher can remove co-authors (except self)

### Postconditions
**Success**: Co-authors linked to publication

### Business Rules
- BR-PUB-001: Corresponding author (owner) cannot be removed
- Co-authors can view but not edit/delete

---

## UC-M1-009: Validate DOI/ISSN

**ID**: UC-M1-009  
**Priority**: 🟡 P1  
**Actor(s)**: System  
**Related User Stories**: US-RES-017, US-RES-018  
**Related FR**: FR-PUB-012, FR-PUB-013

### Goal
Validate DOI and ISSN formats in real-time.

### Main Flow
1. Researcher enters DOI or ISSN
2. Researcher moves to next field (blur event)
3. System validates format:
   - DOI: `^10\\.\\d{4,9}/[-._;()/:A-Z0-9]+$`
   - ISSN: `^\\d{4}-\\d{3}[0-9X]$`
4. If valid: Show green checkmark, create clickable link (DOI)
5. If invalid: Show red error message with format hint

### Postconditions
**Success**: Valid format, link created  
**Failure**: Error shown, must fix before submit

### Business Rules
- BR-PUB-004: DOI and ISSN formats are strictly validated

---

**Tài liệu liên quan**:
- [High-Level UC-HL-001](../High_Level/uc_hl_01_manage_publications.md)
- [User Stories - Researcher](../../04_User_Stories/By_Role/researcher_stories.md)
- [Requirements - Publication Management](../../03_Requirements/Functional/module_publication_management.md)
