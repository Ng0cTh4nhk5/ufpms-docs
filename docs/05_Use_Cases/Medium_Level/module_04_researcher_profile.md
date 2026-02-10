# Module 4: Researcher Profile - Medium-Level Use Cases

> **Module**: 4 - Researcher Profile  
> **High-Level UC**: [UC-HL-004](../High_Level/uc_hl_04_researcher_profile.md)

---

## UC-M4-001: View Public Profile
**ID**: UC-M4-001 | **Priority**: 🟡 P1 | **Actor**: Public Visitor, All Users  
**Related**: US-RES-014, US-VIW-008, FR-PRO-001

**Goal**: View researcher's public profile  
**Preconditions**: None (public access)  
**Main Flow**:
1. User accesses `/profile/[username]`
2. System fetches researcher data
3. System displays profile page:
   - Header: Photo, name, title, faculty
   - Bio: Research interests, contact info
   - External links: ORCID, Google Scholar
   - Publications: PUBLISHED only, sorted by year
   - Analytics charts (if enabled)
4. User can click publications for details

**Postconditions**: Profile displayed  
**Business Rules**: BR-PRO-001 (PUBLISHED only), BR-PRO-005 (SEO)

---

## UC-M4-002: Edit Profile
**ID**: UC-M4-002 | **Priority**: 🟡 P1 | **Actor**: Researcher  
**Related**: US-RES-015, FR-PRO-002

**Goal**: Edit public profile information  
**Preconditions**: User is authenticated, viewing own profile  
**Main Flow**:
1. Researcher clicks "Edit Profile"
2. System displays editable form:
   - Bio (max 500 chars)
   - Research interests
   - ORCID
   - Google Scholar link
   - Personal website
3. Researcher makes changes
4. Researcher clicks "Save"
5. System validates input
6. System updates database
7. System shows "Saved successfully"

**Business Rules**: BR-PRO-002 (only owner can edit)

---

## UC-M4-003: Update Profile Photo
**ID**: UC-M4-003 | **Priority**: 🟡 P1 | **Actor**: Researcher  
**Related**: FR-PRO-002

**Goal**: Upload or change profile photo  
**Main Flow**:
1. Researcher clicks "Edit Profile"
2. Researcher clicks "Change Photo"
3. Researcher selects image file (JPG/PNG, < 2MB)
4. System validates file
5. System auto-resizes to 300x300px
6. System saves photo
7. System displays new photo

**Business Rules**: BR-PRO-004 (formats, size,resize)

---

## UC-M4-004: Link ORCID
**ID**: UC-M4-004 | **Priority**: 🟡 P1 | **Actor**: Researcher  
**Related**: FR-PRO-002

**Goal**: Link ORCID profile  
**Main Flow**:
1. Researcher enters ORCID ID in profile
2. System validates format (0000-0000-0000-000X)
3. System saves ORCID
4. System displays ORCID badge on profile
5. Badge links to `orcid.org/[ORCID]`

**Business Rules**: ORCID format validation

---

## UC-M4-005: View Publication Analytics
**ID**: UC-M4-005 | **Priority**: 🟢 P2 | **Actor**: Researcher, Public Visitor  
**Related**: US-RES-022, FR-PRO-004

**Goal**: View publication productivity charts  
**Main Flow**:
1. User views profile
2. System generates charts:
   - Bar chart: Publications per year
   - Pie chart: Distribution by quartile
3. Charts are interactive (hover for counts)
4. Data updates when new publications published

**Business Rules**: Based on PUBLISHED publications only

---

## UC-M4-006: Generate Word Cloud
**ID**: UC-M4-006 | **Priority**: 🟢 P2 | **Actor**: Researcher, Public Visitor   **Related**: US-RES-023, FR-PRO-005

**Goal**: Visualize research areas via word cloud  
**Main Flow**:
1. User views profile
2. System extracts keywords from all publications
3. System calculates frequency
4. System generates word cloud (font size = frequency)
5. System displays on profile

**Business Rules**: Keywords from PUBLISHED publications

---

**Tài liệu liên quan**:
- [High-Level UC-HL-004](../High_Level/uc_hl_04_researcher_profile.md)
- [User Stories - Researcher](../../04_User_Stories/By_Role/researcher_stories.md)
- [Requirements - Profile](../../03_Requirements/Functional/module_profile.md)
