# Publication Creation Workflow - Activity Diagram

> 📊 **Diagram**: Publication Creation  
> 🎯 **Scope**: Create và save publication  
> 👤 **Actor**: Researcher

---

## 📊 Activity Diagram

```mermaid
flowchart TD
    Start([Researcher clicks<br/>"Create Publication"]) --> LoadForm[Load creation form]
    
    LoadForm --> GetMetadata[Fetch metadata options<br/>from database]
    GetMetadata --> DisplayForm[Display empty form]
    
    DisplayForm --> FillBasic{Fill basic info?}
    
    FillBasic -->|Enter data| EnterTitle[Enter title]
    EnterTitle --> EnterJournal[Enter journal/conference]
    EnterJournal --> EnterYear[Enter year]
    EnterYear --> SelectType[Select publication type]
    SelectType --> EnterDOI[Enter DOI optional]
    
    EnterDOI --> FillAuthors{Add authors?}
    
    FillAuthors -->|Yes| AddAuthor[Add author<br/>name, order, affiliation]
    AddAuthor --> MoreAuthors{More authors?}
    MoreAuthors -->|Yes| AddAuthor
    MoreAuthors -->|No| FillAbstract
    
    FillAuthors -->|Skip| FillAbstract[Enter abstract optional]
    
    FillAbstract --> FillKeywords[Enter keywords optional]
    
    FillKeywords --> UploadPDF{Upload PDF?}
    
    UploadPDF -->|Yes| SelectFile[Select PDF file]
    SelectFile --> ValidateFile{File valid?}
    
    ValidateFile -->|No: >10MB or not PDF| ShowError1[Show error message]
    ShowError1 --> SelectFile
    
    ValidateFile -->|Yes| UploadFile[Upload to server]
    UploadFile --> SavePath[Save file path]
    SavePath --> Decision
    
    UploadPDF -->|No| Decision{Action?}
    
    Decision -->|Save as Draft| ValidateDraft{Required fields<br/>filled?}
    
    ValidateDraft -->|No: Title missing| ShowError2[Show validation errors]
    ShowError2 --> EnterTitle
    
    ValidateDraft -->|Yes| CheckDuplicate[Check duplicate DOI<br/>if provided]
    
    CheckDuplicate -->|Duplicate found| ShowError3[Show error:<br/>"DOI exists"]
    ShowError3 --> EnterDOI
    
    CheckDuplicate -->|No duplicate| SaveDraft[Save to database<br/>Status: DRAFT]
    SaveDraft --> Success1[Show success message]
    Success1 --> End1([Redirect to<br/>My Publications])
    
    Decision -->|Cancel| Confirm{Confirm discard?}
    Confirm -->|Yes| End2([Return to dashboard])
    Confirm -->|No| DisplayForm
    
    style Start fill:#e3f2fd
    style End1 fill:#c8e6c9
    style End2 fill:#ffccbc
    style SaveDraft fill:#fff9c4
    style ShowError1 fill:#ffcdd2
    style ShowError2 fill:#ffcdd2
    style ShowError3 fill:#ffcdd2
```

---

## 📋 Steps Detail

### 1. Load Form
- Fetch publication types (Journal, Conference, Book Chapter, etc.)
- Fetch subject areas
- Display empty form

### 2. Fill Basic Information
**Required**:
- Title (min 10 chars)

**Optional but important**:
- Journal/Conference name
- Year (1900-current year)
- Publication type
- DOI
- ISSN

### 3. Add Authors
- Researcher (owner) auto-added as first author
- Can add co-authors:
  - Name
  - Order (1, 2, 3...)
  - Affiliation
  - Corresponding author checkbox

### 4. Additional Information
- Abstract (recommended, min 100 chars)
- Keywords (comma-separated)
- URL (optional)

### 5. Upload PDF
- File size: max 10MB
- Format: PDF only
- Validation on client + server

### 6. Save as Draft
**Validation**:
- Title required
- At least 1 author (owner)
- DOI uniqueness check (if provided)

**Database**:
- INSERT into publications (status = DRAFT)
- INSERT into publication_authors
- Set created_at = now()

---

## ⏱️ Average Time

- Quick draft (title only): ~30 seconds
- Complete info (no PDF): ~3-5 minutes
- Full publication (with PDF): ~5-10 minutes

---

## 🚨 Error Scenarios

### 1. Validation Errors
- Title too short
- Invalid year
- Invalid URL format

### 2. File Upload Errors
- File too large (>10MB)
- Not a PDF file
- Upload failed (network issue)

### 3. Duplicate DOI
- DOI already exists in system
- User must change DOI or contact admin

---

## 💡 Business Rules

1. **Auto-save** (P1): Draft auto-saved every 60 seconds
2. **PDF later**: Can save draft without PDF, upload later
3. **Edit anytime**: Can edit DRAFT publications
4. **Required for submission**: PDF + complete info required before submit

---

**Related**: UC-D1-01, seq_create_publication.md  
**Created**: 11/02/2026
