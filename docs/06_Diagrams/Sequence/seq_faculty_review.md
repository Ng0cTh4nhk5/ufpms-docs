# Biểu đồ Tuần tự: Quy trình Đánh giá cấp Khoa

> 📊 **ID Biểu đồ**: SEQ-03  
> 🎯 **Ca Sử Dụng**: UC-D2-05 - Đánh giá Khoa  
> 👤 **Tác nhân**: Người đánh giá Khoa  
> ⚙️ **Chính**: Đánh giá, Phê duyệt/Từ chối/Yêu cầu Chỉnh sửa

---

## 📊 Biểu đồ Tuần tự

```mermaid
sequenceDiagram
    actor Reviewer as 👨‍💼 Người đánh giá Khoa
    participant UI as 🖥️ Giao diện React
    participant API as 🔌 WorkflowController
    participant Service as ⚙️ WorkflowService
    participant Repo as 💾 Repository
    participant DB as 🗄️ CSDL
    participant Notif as 📧 Dịch vụ Thông báo
    
    %% Xem danh sách bài gửi
    Reviewer->>UI: Điều hướng đến "Đánh giá của Tôi"
    UI->>API: GET /api/reviews/pending
    API->>Service: getPendingReviews(reviewerId)
    Service->>Repo: findByFacultyAndStatus(facultyId, "FACULTY_REVIEWING")
    Repo->>DB: SELECT * WHERE faculty_id = ?<br/>AND status = 'FACULTY_REVIEWING'
    DB-->>Repo: Danh sách ấn phẩm
    Repo-->>Service: Ấn phẩm[]
    Service-->>API: Ấn phẩm
    API-->>UI: Danh sách đánh giá đang chờ
    UI-->>Reviewer: Hiển thị danh sách
    
    %% Xem chi tiết
    Reviewer->>UI: Nhấn vào ấn phẩm
    UI->>API: GET /api/publications/{id}
    API->>Repo: findById(id)
    Repo->>DB: SELECT với tác giả, PDF
    DB-->>Repo: Dữ liệu ấn phẩm đầy đủ
    Repo-->>API: Ấn phẩm
    API-->>UI: Chi tiết ấn phẩm
    UI-->>Reviewer: Hiển thị chi tiết + Trình xem PDF
    
    %% Thêm bình luận
    Reviewer->>UI: Nhập bình luận đánh giá
    Reviewer->>UI: Chọn hành động: Phê duyệt/Chỉnh sửa/Từ chối
    
    alt Hành động: Phê duyệt
        Reviewer->>UI: Nhấn "Phê duyệt"
        UI->>API: POST /api/reviews/{id}/approve
        activate API
        
        API->>Service: approveAtFaculty(pubId, reviewerId, comments)
        activate Service
        
        Note over Service,DB: BẮT ĐẦU GIAO DỊCH
        
        %% Cập nhật trạng thái
        Service->>Repo: updateStatus(pubId, "FACULTY_APPROVED")
        Repo->>DB: UPDATE publications<br/>SET status = 'FACULTY_APPROVED'
        
        %% Tự động chuyển sang đánh giá cấp trường
        Service->>Repo: updateStatus(pubId, "UNIVERSITY_REVIEWING")
        Repo->>DB: UPDATE publications<br/>SET status = 'UNIVERSITY_REVIEWING'
        
        %% Ghi lịch sử đánh giá
        Service->>Repo: createReviewHistory(entry)
        Repo->>DB: INSERT INTO review_history
        
        %% Lưu bình luận
        alt Có bình luận
            Service->>Repo: saveComments(pubId, reviewerId, comments)
            Repo->>DB: INSERT INTO review_comments
        end
        
        Note over Service,DB: CAM KẾT
        
        %% Thông báo
        Service->>Notif: notifyFacultyApproval(publication)
        activate Notif
        Notif->>Notif: Thông báo cho nhà nghiên cứu (đã phê duyệt)
        Notif->>Notif: Thông báo cho người đánh giá trường (nhiệm vụ mới)
        deactivate Notif
        
        Service-->>API: Thành công
        deactivate Service
        API-->>UI: 200 OK
        deactivate API
        UI-->>Reviewer: "Đã phê duyệt thành công"
        
    else Hành động: Yêu cầu Chỉnh sửa
        Reviewer->>UI: Nhấn "Yêu cầu Chỉnh sửa"
        UI->>UI: Yêu cầu bình luận
        Reviewer->>UI: Nhập lý do chỉnh sửa
        
        UI->>API: POST /api/reviews/{id}/request-revision
        activate API
        API->>Service: requestRevision(pubId, reviewerId, comments)
        activate Service
        
        Note over Service,DB: BẮT ĐẦU GIAO DỊCH
        
        Service->>Repo: updateStatus(pubId, "REVISION_REQUIRED")
        Repo->>DB: UPDATE publications<br/>SET status = 'REVISION_REQUIRED'
        
        Service->>Repo: saveComments(pubId, reviewerId, comments)
        Repo->>DB: INSERT INTO review_comments
        
        Service->>Repo: createReviewHistory(entry)
        Repo->>DB: INSERT INTO review_history
        
        Note over Service,DB: CAM KẾT
        
        Service->>Notif: notifyRevisionRequired(publication, comments)
        activate Notif
        Notif->>Notif: Gửi email cho nhà nghiên cứu kèm bình luận
        deactivate Notif
        
        Service-->>API: Thành công
        deactivate Service
        API-->>UI: 200 OK
        deactivate API
        UI-->>Reviewer: "Đã yêu cầu chỉnh sửa"
        
    else Hành động: Từ chối
        Reviewer->>UI: Nhấn "Từ chối"
        UI->>UI: Yêu cầu lý do từ chối
        Reviewer->>UI: Nhập lý do
        
        UI->>API: POST /api/reviews/{id}/reject
        activate API
        API->>Service: rejectPublication(pubId, reviewerId, reason)
        activate Service
        
        Note over Service,DB: BẮT ĐẦU GIAO DỊCH
        
        Service->>Repo: updateStatus(pubId, "REJECTED")
        Repo->>DB: UPDATE publications<br/>SET status = 'REJECTED'
        
        Service->>Repo: saveComments(pubId, reviewerId, reason)
        Repo->>DB: INSERT INTO review_comments
        
        Service->>Repo: createReviewHistory(entry)
        Repo->>DB: INSERT INTO review_history
        
        Note over Service,DB: CAM KẾT
        
        Service->>Notif: notifyRejection(publication, reason)
        activate Notif
        Notif->>Notif: Gửi email cho nhà nghiên cứu
        deactivate Notif
        
        Service-->>API: Thành công
        deactivate Service
        API-->>UI: 200 OK
        deactivate API
        UI-->>Reviewer: "Ấn phẩm bị từ chối"
    end
```

---

## 📋 Ba Hành Động

### 1. Phê duyệt ✅
- Trạng thái: `FACULTY_REVIEWING` → `FACULTY_APPROVED` → `UNIVERSITY_REVIEWING`
- Thông báo: Nhà nghiên cứu (đã phê duyệt) + Người đánh giá Trường (nhiệm vụ mới)
- Bình luận tùy chọn

### 2. Yêu cầu Chỉnh sửa 📝
- Trạng thái: `FACULTY_REVIEWING` → `REVISION_REQUIRED`
- Nhà nghiên cứu có thể chỉnh sửa lại → gửi lại
- Bình luận **bắt buộc**

### 3. Từ chối ❌
- Trạng thái: `FACULTY_REVIEWING` → `REJECTED`
- Từ chối cuối cùng (không thể gửi lại nếu không có SuperAdmin)
- Lý do **bắt buộc**

---

## 🗄️ Thay Đổi Cơ Sở Dữ Liệu

### Phê duyệt
```sql
-- Chuyển đổi trạng thái
UPDATE publications SET status = 'FACULTY_APPROVED' WHERE id = ?;
UPDATE publications SET status = 'UNIVERSITY_REVIEWING' WHERE id = ?;

-- Lịch sử
INSERT INTO review_history (publication_id, from_status, to_status, actor_id, action, comments)
VALUES (?, 'FACULTY_REVIEWING', 'UNIVERSITY_REVIEWING', ?, 'APPROVE', ?);
```

### Yêu cầu Chỉnh sửa
```sql
UPDATE publications SET status = 'REVISION_REQUIRED' WHERE id = ?;

INSERT INTO review_comments (publication_id, reviewer_id, comment_type, comment_text)
VALUES (?, ?, 'REVISION_REQUEST', ?);

INSERT INTO review_history ...
```

### Từ chối
```sql
UPDATE publications SET status = 'REJECTED' WHERE id = ?;

INSERT INTO review_comments (publication_id, reviewer_id, comment_type, comment_text)
VALUES (?, ?, 'REJECTION_REASON', ?);

INSERT INTO review_history ...
```

---

**Liên quan**: FR-APR-005 đến APR-009, US-FCR-002 đến FCR-005  
**Ngày tạo**: 10/02/2026
