# Complete Approval Workflow - Activity Diagram

> 📊 **Diagram**: Complete Approval Workflow  
> ⚙️ **States**: 9 states với decision points  
> 👥 **Swimlanes**: Researcher, Faculty Reviewer, University Reviewer

---

## 📊 Activity Diagram

```mermaid
flowchart TD
    Start([Start: Create Publication]) --> Draft[Status: DRAFT]
    
    Draft --> EditLoop{Continue<br/>editing?}
    EditLoop -->|Yes| Edit[Edit Publication]
    Edit --> Draft
    EditLoop -->|No| Submit[Submit for Review]
    
    Submit --> Submitted[Status: SUBMITTED]
    Submitted --> FacReview[Status: FACULTY_REVIEWING]
    
    FacReview --> FacDecision{Faculty<br/>Decision?}
    
    FacDecision -->|Approve| FacApproved[Status: FACULTY_APPROVED]
    FacDecision -->|Request Revision| Revision[Status: REVISION_REQUIRED]
    FacDecision -->|Reject| Rejected[Status: REJECTED]
    
    Revision --> ResearcherFix[Researcher fixes issues]
    ResearcherFix --> Draft
    
    FacApproved --> UniReview[Status: UNIVERSITY_REVIEWING]
    
    UniReview --> UniDecision{University<br/>Decision?}
    
    UniDecision -->|Approve| Published[Status: PUBLISHED]
    UniDecision -->|Send Back| FacReview
    
    Published --> End([End: Public])
    Rejected --> End2([End: Rejected])
    
    style Draft fill:#fff9c4
    style Submitted fill:#ffcc80
    style FacReview fill:#ffab91
    style FacApproved fill:#a5d6a7
    style Revision fill:#ef9a9a
    style Rejected fill:#e57373
    style UniReview fill:#ce93d8
    style Published fill:#81c784
```

---

## 📋 Workflow States

1. **DRAFT** - Researcher editing
2. **SUBMITTED** - Acknowledged
3. **FACULTY_REVIEWING** - At faculty level
4. **FACULTY_APPROVED** - Faculty approved
5. **UNIVERSITY_REVIEWING** - At university level
6. **PUBLISHED** - Final, public
7. **REVISION_REQUIRED** - Needs changes
8. **REJECTED** - Final rejection
9. **WITHDRAWN** - Researcher withdrew (not shown)

---

## 🎯 Decision Points

### Faculty Decision
- ✅ **Approve** → UNIVERSITY_REVIEWING
- 📝 **Request Revision** → REVISION_REQUIRED (Researcher can re-edit)
- ❌ **Reject** → REJECTED (final, cannot resubmit)

### University Decision
- ✅ **Approve** → PUBLISHED (public!)
- 🔄 **Send Back** → FACULTY_REVIEWING (re-review)

---

## ⏱️ Average Timeline

- DRAFT → SUBMITTED: Variable (researcher)
- FACULTY_REVIEWING: 3-7 days
- UNIVERSITY_REVIEWING: 3-7 days
- **Total SLA**: 6-14 days (submit → publish)

---

**Related**: UC-M2 (Approval Workflow), seq_faculty_review.md, seq_university_approval.md  
**Created**: 10/02/2026
