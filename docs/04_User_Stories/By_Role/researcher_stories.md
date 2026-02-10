# User Stories - Researcher

> 👤 **Role**: Researcher (Giảng viên)  
> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Mục tiêu**: Quản lý bài báo khoa học và theo dõi tiến độ phê duyệt

---

## Tổng Quan

**Total Stories**: 28  
**P0 (Must Have)**: 18  
**P1 (Should Have)**: 7  
**P2 (Nice to Have)**: 3

---

## Module 1: Publication Management

### US-RES-001: Tạo Bài Báo Mới
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-PUB-001

**User Story**:
```
As a researcher,
I want to create a new publication entry with required metadata,
So that I can submit it for review and eventual publication.
```

**Acceptance Criteria**:
```
GIVEN I am logged in as a researcher
WHEN I click "Add New Publication"
THEN I see a form with required fields (Title, Authors, Year, Journal Type)
AND optional fields (DOI, ISSN, Abstract, Keywords, PDF)
AND the publication status is set to DRAFT by default
```

---

### US-RES-002: Upload File PDF
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-PUB-002

**User Story**:
```
As a researcher,
I want to upload the PDF file of my publication,
So that reviewers and readers can access the full text.
```

**Acceptance Criteria**:
```
GIVEN I am creating or editing a publication
WHEN I select a PDF file (< 10MB) and upload it
THEN the file is uploaded to the server
AND the path is saved to database
AND I see a preview thumbnail
AND I can download it again to verify
```

---

### US-RES-003: Sửa Bài Báo Nháp
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-PUB-004

**User Story**:
```
As a researcher,
I want to edit my draft or revision-required publications,
So that I can correct errors or add missing information.
```

**Acceptance Criteria**:
```
GIVEN my publication is in DRAFT or REVISION_REQUIRED status
AND I am the owner
WHEN I edit the information and click Save
THEN the database is updated
AND an audit log is created (who edited, when)
AND I see "Saved successfully" message
```

---

### US-RES-004: Xóa Bài Báo Nháp
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-PUB-005

**User Story**:
```
As a researcher,
I want to delete my draft publications,
So that I can remove entries I no longer want to submit.
```

**Acceptance Criteria**:
```
GIVEN my publication is in DRAFT status
AND I am the owner
WHEN I click "Delete" and confirm
THEN the publication is soft deleted (deleted_at timestamp set)
AND the PDF file is removed from storage
AND I am redirected to my publications list
```

---

### US-RES-005: Xem Danh Sách Bài Báo
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-PUB-006

**User Story**:
```
As a researcher,
I want to view all my publications filtered by status,
So that I can easily find and manage them.
```

**Acceptance Criteria**:
```
GIVEN I am logged in as a researcher
WHEN I go to "My Publications"
THEN I see my publications list with:
- Filter options: All / Draft / Submitted / Approved / Rejected
- Sort: Newest first
- Columns: Title, Status, Update Date, Actions (Edit/Delete/View)
```

---

### US-RES-006: Thêm Đồng Tác Giả
**Priority**: 🟡 P1 - Should Have  
**Related FR**: FR-PUB-007

**User Story**:
```
As a researcher,
I want to add co-authors from my university to my publication,
So that we are all properly credited for our collaborative work.
```

**Acceptance Criteria**:
```
GIVEN I am creating or editing a publication
WHEN I type a researcher's name in the co-authors field
THEN I see autocomplete suggestions from the system's user list
AND I can add them to the co-authors list
AND I can remove co-authors from the list
AND I cannot remove myself as the corresponding author
```

---

### US-RES-007: Gắn Tags/Keywords
**Priority**: 🟡 P1 - Should Have  
**Related FR**: FR-PUB-008

**User Story**:
```
As a researcher,
I want to add keywords/tags to my publication,
So that it can be easily found through search.
```

**Acceptance Criteria**:
```
GIVEN I am creating or editing a publication
WHEN I enter keywords separated by commas
THEN they are saved as an array
AND displayed as colored tags
AND I can remove individual tags by clicking X
```

---

### US-RES-008: Xem Chi Tiết Bài Báo
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-PUB-010

**User Story**:
```
As a researcher,
I want to view all details of my publication,
So that I can review the complete information and status.
```

**Acceptance Criteria**:
```
GIVEN I have permission to view a publication (owner/admin/reviewer)
WHEN I click "View Details"
THEN I see all metadata, current status, review history (if any),
AND PDF file link (if uploaded)
AND DOI link (if available)
```

---

### US-RES-009: Download File PDF
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-PUB-011

**User Story**:
```
As a researcher,
I want to download the PDF of my publication,
So that I can verify the uploaded file or share it offline.
```

**Acceptance Criteria**:
```
GIVEN the publication has a PDF file
AND I have permission to view it (owner/admin/reviewer/or PUBLISHED)
WHEN I click "Download PDF"
THEN the file is downloaded to my computer
AND an audit log records who downloaded it and when
```

---

## Module 2: Approval Workflow (Researcher Actions)

### US-RES-010: Nộp Xét Duyệt
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-APR-001

**User Story**:
```
As a researcher,
I want to submit my publication for review,
So that it can go through the approval process and be published.
```

**Acceptance Criteria**:
```
GIVEN my publication is in DRAFT status
AND all required fields are filled (Title, Authors, Journal, Year, PDF)
WHEN I click "Submit for Review"
THEN the status changes from DRAFT to SUBMITTED
AND an email is sent to the Faculty Reviewer
AND an audit log is created
AND I see "Submitted successfully" message
```

---

### US-RES-011: Xem Trạng Thái Xét Duyệt
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-APR-002

**User Story**:
```
As a researcher,
I want to track the review status of my submitted publication,
So that I know where it is in the approval process.
```

**Acceptance Criteria**:
```
GIVEN I have submitted a publication
WHEN I view its details
THEN I see a visual timeline: DRAFT → SUBMITTED → REVIEWING → APPROVED
AND the current status is highlighted
AND I can see reviewer comments (if any)
AND the date of each status transition
```

---

### US-RES-012: Chỉnh Sửa Theo Yêu Cầu
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-APR-003

**User Story**:
```
As a researcher,
I want to revise my publication based on reviewer feedback,
So that I can address concerns and resubmit for approval.
```

**Acceptance Criteria**:
```
GIVEN my publication is in REVISION_REQUIRED status
AND there are comments from the reviewer
WHEN I make edits and click "Resubmit"
THEN the status changes from REVISION_REQUIRED to SUBMITTED
AND an email is sent to the Faculty Reviewer: "Revised and resubmitted"
AND an audit log is created
```

---

### US-RES-013: Rút Lại Đơn Nộp
**Priority**: 🟡 P1 - Should Have  
**Related FR**: FR-APR-019

**User Story**:
```
As a researcher,
I want to withdraw my submission before it's approved,
So that I can make significant changes or reconsider submission.
```

**Acceptance Criteria**:
```
GIVEN my publication is in SUBMITTED or FACULTY_REVIEWING status
WHEN I click "Withdraw" and confirm
THEN the status changes back to DRAFT
AND an email is sent to the reviewer (if already reviewing)
AND an audit log is created
```

---

## Module 4: Researcher Profile

### US-RES-014: Xem Profile Công Khai Của Mình
**Priority**: 🟡 P1 - Should Have  
**Related FR**: FR-PRO-001

**User Story**:
```
As a researcher,
I want to view my public profile page,
So that I can see how my information and publications appear to others.
```

**Acceptance Criteria**:
```
GIVEN I have at least 1 PUBLISHED publication
WHEN I access /profile/[my-username]
THEN I see my profile photo, name, title, faculty,
AND contact info (email, ORCID),
AND bio/research interests,
AND list of PUBLISHED publications only,
AND a chart showing publications by year
AND a word cloud from my keywords
```

---

### US-RES-015: Chỉnh Sửa Profile
**Priority**: 🟡 P1 - Should Have  
**Related FR**: FR-PRO-002

**User Story**:
```
As a researcher,
I want to edit my public profile information,
So that I can keep my professional information up to date.
```

**Acceptance Criteria**:
```
GIVEN I am logged in
WHEN I go to "Edit Profile"
THEN I can edit: Profile photo, Bio (max 500 chars), Research interests,
ORCID, Google Scholar link, Personal website
AND changes are saved when I click "Save"
```

---

### US-RES-016: Xem Danh Sách Bài Báo Trên Profile
**Priority**: 🟡 P1 - Should Have  
**Related FR**: FR-PRO-003

**User Story**:
```
As a researcher,
I want my publications displayed on my profile page,
So that visitors can see my research output.
```

**Acceptance Criteria**:
```
GIVEN I am viewing my public profile
WHEN the page loads
THEN I see my publications (PUBLISHED only) sorted by year (newest first)
AND I can filter by type (Journal/Conference)
AND each entry shows: Title, Journal, Year, DOI link
AND visitors can click to view details
```

---

## Advanced Features

### US-RES-017: Validate DOI Format
**Priority**: 🟡 P1 - Should Have  
**Related FR**: FR-PUB-012

**User Story**:
```
As a researcher,
I want the system to validate my DOI format,
So that I don't submit publications with incorrect DOI.
```

**Acceptance Criteria**:
```
GIVEN I am entering a DOI in the publication form
WHEN I move to the next field (blur)
THEN the system validates the format (10.xxxx/xxxxx)
AND shows an error message if incorrect
AND creates a clickable link to https://doi.org/[DOI] if correct
```

---

### US-RES-018: Validate ISSN Format
**Priority**: 🟡 P1 - Should Have  
**Related FR**: FR-PUB-013

**User Story**:
```
As a researcher,
I want the system to validate the ISSN format,
So that I enter correct journal ISSN numbers.
```

**Acceptance Criteria**:
```
GIVEN I am entering an ISSN in the publication form
WHEN I move to the next field
THEN the system validates the format (xxxx-xxxx)
AND shows an error message if incorrect
```

---

### US-RES-019: Cảnh Báo Trùng Lặp
**Priority**: 🟡 P1 - Should Have  
**Related FR**: FR-PUB-014

**User Story**:
```
As a researcher,
I want to be notified if a publication with the same DOI already exists,
So that I can add myself as co-author instead of creating a duplicate.
```

**Acceptance Criteria**:
```
GIVEN I enter a DOI that already exists in the system
WHEN I save the publication
THEN I see a warning: "This publication has been entered by [Researcher Name]"
AND a suggestion: "Would you like to add yourself as co-author?"
```

---

### US-RES-020: Auto-Fetch Metadata từ DOI
**Priority**: 🟢 P2 - Nice to Have  
**Related FR**: FR-PUB-003

**User Story**:
```
As a researcher,
I want to automatically fetch publication metadata from DOI,
So that I don't have to manually enter all information.
```

**Acceptance Criteria**:
```
GIVEN I have entered a valid DOI (10.xxxx/xxxxx)
WHEN I click "Fetch from DOI"
THEN the system calls CrossRef API
AND auto-fills: Title, Authors, Journal, Year, ISSN
AND allows me to manually edit the auto-filled data
```

---

### US-RES-021: Import từ ORCID
**Priority**: 🟢 P2 - Nice to Have  
**Related FR**: FR-PUB-015

**User Story**:
```
As a researcher,
I want to import my publications from my ORCID profile,
So that I can quickly add my existing publications to the system.
```

**Acceptance Criteria**:
```
GIVEN I have linked my ORCID account
WHEN I click "Import from ORCID"
THEN the system calls ORCID API
AND displays a list of my publications
AND I can select which ones to import
AND metadata is auto-filled for selected publications
```

---

### US-RES-022: Xem Biểu Đồ Năng Suất
**Priority**: 🟢 P2 - Nice to Have  
**Related FR**: FR-PRO-004

**User Story**:
```
As a researcher,
I want to see charts of my publication productivity,
So that I can visualize my research output over time.
```

**Acceptance Criteria**:
```
GIVEN I am viewing my profile
WHEN the analytics section loads
THEN I see:
- Bar chart: Publications per year
- Pie chart: Publications by journal type (Q1/Q2/Q3/Q4/Conference)
- Highlight: Most productive years
```

---

### US-RES-023: Xem Word Cloud Lĩnh Vực
**Priority**: 🟢 P2 - Nice to Have  
**Related FR**: FR-PRO-005

**User Story**:
```
As a researcher,
I want to see a word cloud of my research fields,
So that I can visualize my areas of expertise.
```

**Acceptance Criteria**:
```
GIVEN I am viewing my profile
WHEN the page loads
THEN I see a word cloud generated from:
- Keywords of all my publications
- Frequent words in abstracts
AND font size is based on frequency
```

---

## Traceability Matrix

| Story ID | Title | Priority | FR ID | Module |
|----------|-------|----------|-------|--------|
| US-RES-001 | Tạo Bài Báo Mới | P0 | FR-PUB-001 | 1 |
| US-RES-002 | Upload File PDF | P0 | FR-PUB-002 | 1 |
| US-RES-003 | Sửa Bài Báo Nháp | P0 | FR-PUB-004 | 1 |
| US-RES-004 | Xóa Bài Báo Nháp | P0 | FR-PUB-005 | 1 |
| US-RES-005 | Xem Danh Sách Bài Báo | P0 | FR-PUB-006 | 1 |
| US-RES-006 | Thêm Đồng Tác Giả | P1 | FR-PUB-007 | 1 |
| US-RES-007 | Gắn Tags/Keywords | P1 | FR-PUB-008 | 1 |
| US-RES-008 | Xem Chi Tiết Bài Báo | P0 | FR-PUB-010 | 1 |
| US-RES-009 | Download File PDF | P0 | FR-PUB-011 | 1 |
| US-RES-010 | Nộp Xét Duyệt | P0 | FR-APR-001 | 2 |
| US-RES-011 | Xem Trạng Thái Xét Duyệt | P0 | FR-APR-002 | 2 |
| US-RES-012 | Chỉnh Sửa Theo Yêu Cầu | P0 | FR-APR-003 | 2 |
| US-RES-013 | Rút Lại Đơn Nộp | P1 | FR-APR-019 | 2 |
| US-RES-014 | Xem Profile Công Khai | P1 | FR-PRO-001 | 4 |
| US-RES-015 | Chỉnh Sửa Profile | P1 | FR-PRO-002 | 4 |
| US-RES-016 | Xem Danh Sách Bài Báo Trên Profile | P1 | FR-PRO-003 | 4 |
| US-RES-017 | Validate DOI Format | P1 | FR-PUB-012 | 1 |
| US-RES-018 | Validate ISSN Format | P1 | FR-PUB-013 | 1 |
| US-RES-019 | Cảnh Báo Trùng Lặp | P1 | FR-PUB-014 | 1 |
| US-RES-020 | Auto-Fetch Metadata từ DOI | P2 | FR-PUB-003 | 1 |
| US-RES-021 | Import từ ORCID | P2 | FR-PUB-015 | 1 |
| US-RES-022 | Xem Biểu Đồ Năng Suất | P2 | FR-PRO-004 | 4 |
| US-RES-023 | Xem Word Cloud Lĩnh Vực | P2 | FR-PRO-005 | 4 |

---

**Tài liệu liên quan**:
- [Requirements - Publication Management](../../03_Requirements/Functional/module_publication_management.md)
- [Requirements - Approval Workflow](../../03_Requirements/Functional/module_approval_workflow.md)
- [Requirements - Researcher Profile](../../03_Requirements/Functional/module_profile.md)
