# Quy Trình Phê Duyệt Hoàn Chỉnh - Biểu đồ Hoạt động

> 📊 **Biểu đồ**: Quy trình Phê duyệt Hoàn chỉnh  
> ⚙️ **Trạng thái**: 9 trạng thái với các điểm quyết định  
> 👥 **Làn bơi (Swimlanes)**: Nhà nghiên cứu, Người đánh giá cấp Khoa, Người đánh giá cấp Trường

---

## 📊 Biểu đồ Hoạt động

```mermaid
flowchart TD
    Start([Bắt đầu: Tạo Ấn phẩm]) --> Draft[Trạng thái: DRAFT (Nháp)]
    
    Draft --> EditLoop{Tiếp tục chỉnh sửa?}
    EditLoop -->|Có| Edit[Chỉnh sửa Ấn phẩm]
    Edit --> Draft
    EditLoop -->|Không| Submit[Gửi đi Đánh giá]
    
    Submit --> Submitted[Trạng thái: SUBMITTED (Đã gửi)]
    Submitted --> FacReview[Trạng thái: FACULTY_REVIEWING (Khoa đang duyệt)]
    
    FacReview --> FacDecision{Quyết định của Khoa?}
    
    FacDecision -->|Phê duyệt| FacApproved[Trạng thái: FACULTY_APPROVED (Khoa đã duyệt)]
    FacDecision -->|Yêu cầu Chỉnh sửa| Revision[Trạng thái: REVISION_REQUIRED (Cần chỉnh sửa)]
    FacDecision -->|Từ chối| Rejected[Trạng thái: REJECTED (Bị từ chối)]
    
    Revision --> ResearcherFix[Nhà nghiên cứu sửa lỗi]
    ResearcherFix --> Draft
    
    FacApproved --> UniReview[Trạng thái: UNIVERSITY_REVIEWING (Trường đang duyệt)]
    
    UniReview --> UniDecision{Quyết định của Trường?}
    
    UniDecision -->|Phê duyệt| Published[Trạng thái: PUBLISHED (Đã xuất bản)]
    UniDecision -->|Gửi lại| FacReview
    
    Published --> End([Kết thúc: Công khai])
    Rejected --> End2([Kết thúc: Bị từ chối])
    
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

## 📋 Trạng Thái Quy Trình

1. **DRAFT** - Nhà nghiên cứu đang chỉnh sửa
2. **SUBMITTED** - Đã ghi nhận
3. **FACULTY_REVIEWING** - Đang ở cấp Khoa
4. **FACULTY_APPROVED** - Khoa đã phê duyệt
5. **UNIVERSITY_REVIEWING** - Đang ở cấp Trường
6. **PUBLISHED** - Cuối cùng, công khai
7. **REVISION_REQUIRED** - Cần thay đổi
8. **REJECTED** - Từ chối cuối cùng
9. **WITHDRAWN** - Nhà nghiên cứu đã rút (không hiển thị)

---

## 🎯 Các Điểm Quyết Định

### Quyết định của Khoa
- ✅ **Phê duyệt** → UNIVERSITY_REVIEWING (Trường đang duyệt)
- 📝 **Yêu cầu Chỉnh sửa** → REVISION_REQUIRED (Nhà nghiên cứu có thể chỉnh sửa lại)
- ❌ **Từ chối** → REJECTED (cuối cùng, không thể gửi lại)

### Quyết định của Trường
- ✅ **Phê duyệt** → PUBLISHED (công khai!)
- 🔄 **Gửi lại** → FACULTY_REVIEWING (đánh giá lại)

---

## ⏱️ Thời Gian Trung Bình

- DRAFT → SUBMITTED: Biến động (nhà nghiên cứu)
- FACULTY_REVIEWING: 3-7 ngày
- UNIVERSITY_REVIEWING: 3-7 ngày
- **Tổng SLA**: 6-14 ngày (gửi → xuất bản)

---

**Liên quan**: UC-M2 (Quy trình Phê duyệt), seq_faculty_review.md, seq_university_approval.md  
**Ngày tạo**: 10/02/2026
