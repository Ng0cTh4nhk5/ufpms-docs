# Biểu đồ Tuần tự: Luồng Yêu cầu Chỉnh sửa

> 📊 **ID Biểu đồ**: SEQ-05  
> 🎯 **Luồng Thay Thế**: Yêu cầu Chỉnh sửa  
> 👤 **Tác nhân**: Người đánh giá → Nhà nghiên cứu  
> ⚙️ **Kết quả**: Nhà nghiên cứu chỉnh sửa và gửi lại

---

## 📊 Biểu đồ Tuần tự

```mermaid
sequenceDiagram
    actor Researcher as 👨‍🔬 Nhà nghiên cứu
    participant UI as 🖥️ Giao diện
    participant API as 🔌 API
    participant Service as ⚙️ Dịch vụ
    participant Repo as 💾 Repository
    participant DB as 🗄️ CSDL
    participant Notif as 📧 Thông báo
    
    Note over Researcher: Ấn phẩm đang ở trạng thái<br/>REVISION_REQUIRED<br/>(người đánh giá yêu cầu thay đổi)
    
    %% Bước 1: Nhận thông báo
    Notif->>Researcher: Email: "Đã yêu cầu chỉnh sửa"
    Researcher->>UI: Nhấn vào liên kết trong email
    
    %% Xem yêu cầu chỉnh sửa
    UI->>API: GET /api/publications/{id}
    API->>Repo: findWithComments(id)
    Repo->>DB: SELECT publication, review_comments
    DB-->>Repo: Dữ liệu
    Repo-->>API: Ấn phẩm + Bình luận
    API-->>UI: Dữ liệu đầy đủ
    UI-->>Researcher: Hiển thị ấn phẩm +<br/>banner vàng: "Yêu cầu Chỉnh sửa"<br/>+ bình luận của người đánh giá
    
    %% Đọc bình luận
    Researcher->>UI: Đọc bình luận
    Note over UI: Hiển thị bình luận:<br/>- Từ khoa/trường<br/>- Yêu cầu chỉnh sửa<br/>- Đề xuất
    
    %% Chỉnh sửa để giải quyết
    Researcher->>UI: Nhấn "Chỉnh sửa để Giải quyết Bình luận"
    UI->>API: POST /api/publications/{id}/start-revision
    API->>Service: changeStatusToDraft(pubId)
    activate Service
    Service->>Repo: updateStatus(pubId, "DRAFT")
    Repo->>DB: UPDATE publications<br/>SET status = 'DRAFT'
    Service->>Repo: logHistory(...)
    Repo->>DB: INSERT review_history<br/>(REVISION_REQUIRED → DRAFT)
    Service-->>API: Thành công
    deactivate Service
    API-->>UI: 200 OK
    UI-->>Researcher: Biểu mẫu chỉnh sửa được bật
    
    %% Thực hiện thay đổi
    Researcher->>UI: Thực hiện thay đổi dựa trên bình luận
    Note over Researcher,UI: Sửa tiêu đề, tóm tắt,<br/>thêm thông tin thiếu, v.v.
    
    Researcher->>UI: Nhấn "Lưu Thay đổi"
    UI->>API: PUT /api/publications/{id}
    API->>Service: updatePublication(id, data)
    Service->>Repo: update(publication)
    Repo->>DB: UPDATE publications
    Repo-->>Service: Đã cập nhật
    Service-->>API: Thành công
    API-->>UI: 200 OK
    UI-->>Researcher: "Đã lưu thay đổi"
    
    %% Gửi lại
    Researcher->>UI: Nhấn "Gửi lại để Đánh giá"
    UI->>API: POST /api/publications/{id}/resubmit
    activate API
    API->>Service: resubmitAfterRevision(pubId, userId)
    activate Service
    
    %% Xác thực hoàn thành lại
    Service->>Service: validateCompletion()
    
    alt Chưa hoàn thành
        Service-->>API: ValidationError
        API-->>UI: 400 + trường thiếu
        UI-->>Researcher: "Vui lòng hoàn thành: ..."
    else Hoàn thành
        Note over Service,DB: BẮT ĐẦU GIAO DỊCH
        
        %% Chuyển đổi trạng thái
        Service->>Repo: updateStatus(pubId, "SUBMITTED")
        Repo->>DB: UPDATE status = 'SUBMITTED'
        
        Service->>Repo: updateStatus(pubId, "FACULTY_REVIEWING")
        Repo->>DB: UPDATE status = 'FACULTY_REVIEWING'
        
        %% Ghi nhật ký gửi lại
        Service->>Repo: logHistory(...)
        Repo->>DB: INSERT review_history<br/>(hành động: RESUBMIT_AFTER_REVISION)
        
        Note over Service,DB: CAM KẾT
        
        %% Thông báo cho cùng người đánh giá
        Service->>Notif: notifyResubmission(publication)
        activate Notif
        Note over Notif: Thông báo cho người đánh giá gốc<br/>(người đã yêu cầu chỉnh sửa)
        Notif->>Notif: Gửi email với cờ "Đã gửi lại"
        deactivate Notif
        
        Service-->>API: Thành công
        deactivate Service
        API-->>UI: 200 OK
        deactivate API
        UI-->>Researcher: "Đã gửi lại thành công!"
    end
```

---

## 📋 Các Bước Luồng

### 1. Thông báo
- Nhà nghiên cứu nhận email: "Đã yêu cầu chỉnh sửa"
- Email chứa:
  - Bình luận của người đánh giá
  - Liên kết đến ấn phẩm
  - Hạn chót (nếu có - P2)

### 2. Xem Bình luận
- Trạng thái ấn phẩm = `REVISION_REQUIRED`
- Giao diện hiển thị banner vàng: "Yêu cầu Chỉnh sửa"
- Hiển thị tất cả bình luận đánh giá từ người đánh giá

### 3. Bắt đầu Chỉnh sửa
- Nhấn "Chỉnh sửa để Giải quyết Bình luận"
- Trạng thái chuyển lại thành `DRAFT`
- Biểu mẫu chỉnh sửa được bật
- Bình luận vẫn hiển thị để tham khảo

### 4. Thực hiện Thay đổi
- Nhà nghiên cứu giải quyết từng bình luận
- Có thể đánh dấu bình luận là "Đã giải quyết" (P2)
- Lưu thay đổi dần dần

### 5. Gửi lại
- Nhấn "Gửi lại để Đánh giá"
- Hệ thống xác thực hoàn thành (giống như lần gửi đầu tiên)
- Trạng thái: `DRAFT` → `SUBMITTED` → `FACULTY_REVIEWING`
- Cờ: Đây là lần gửi lại (không phải mới)

### 6. Đánh giá lại
- Quay lại **cùng người đánh giá**
- Người đánh giá có thể thấy:
  - Bình luận gốc
  - Những gì đã thay đổi (diff - P2)
  - Đây là một bản gửi lại sau chỉnh sửa

---

## 📧 Thông báo Email

### Đến Nhà nghiên cứu (Yêu cầu Chỉnh sửa)
```
Chủ đề: Yêu cầu chỉnh sửa - {title}

Thân gửi {researcher_name},

Người đánh giá đã yêu cầu chỉnh sửa cho ấn phẩm của bạn:

Tiêu đề: {title}
Người đánh giá: {reviewer_name}
Ngày: {timestamp}

Bình luận:
{comments}

Vui lòng thực hiện các thay đổi cần thiết và gửi lại.

Xem ấn phẩm: {url}

Trân trọng,
UFPMS
```

### Đến Người đánh giá (Đã gửi lại)
```
Chủ đề: Ấn phẩm đã được gửi lại - {title}

Thân gửi {reviewer_name},

Ấn phẩm bạn yêu cầu chỉnh sửa đã được gửi lại:

Tiêu đề: {title}
Nhà nghiên cứu: {researcher_name}
Đã gửi lại: {timestamp}

Bình luận gốc: {original_comments}

Vui lòng đánh giá: {url}

Trân trọng,
UFPMS
```

---

## 🗄️ Thay Đổi Cơ Sở Dữ Liệu

### Bắt đầu Chỉnh sửa
```sql
UPDATE publications 
SET status = 'DRAFT'
WHERE id = ? AND status = 'REVISION_REQUIRED';

INSERT INTO review_history (
    publication_id, from_status, to_status,
    actor_id, action
) VALUES (
    ?, 'REVISION_REQUIRED', 'DRAFT',
    ?, 'START_REVISION'
);
```

### Gửi lại Sau khi Chỉnh sửa
```sql
UPDATE publications 
SET status = 'FACULTY_REVIEWING'
WHERE id = ? AND status = 'DRAFT';

INSERT INTO review_history (
    publication_id, from_status, to_status,
    actor_id, action, is_resubmission
) VALUES (
    ?, 'DRAFT', 'FACULTY_REVIEWING',
    ?, 'RESUBMIT_AFTER_REVISION', TRUE
);
```

---

## 🔄 Chuyển đổi Trạng thái

```mermaid
stateDiagram-v2
    FACULTY_REVIEWING --> REVISION_REQUIRED: Yêu cầu Chỉnh sửa
    REVISION_REQUIRED --> DRAFT: Bắt đầu Chỉnh sửa
    DRAFT --> DRAFT: Lưu Thay đổi
    DRAFT --> SUBMITTED: Gửi lại
    SUBMITTED --> FACULTY_REVIEWING: Tự động
    
    note right of FACULTY_REVIEWING
        Quay lại cùng người đánh giá
        Được gắn cờ là gửi lại
    end note
```

---

## 💡 Quy Tắc Nghiệp Vụ

1. **Nhà nghiên cứu có thể chỉnh sửa không giới hạn lần** khi ở trạng thái DRAFT
2. **Cho phép nhiều lần chỉnh sửa**: Người đánh giá có thể yêu cầu chỉnh sửa lại
3. **Theo dõi hạn chót** (P2): Gửi nhắc nhở nếu không gửi lại trong X ngày
4. **Số lần chỉnh sửa**: Theo dõi số lần đã chỉnh sửa (để phân tích)

---

**Liên quan**: FR-APR-008, FR-APR-003, US-RES-012, US-FCR-004  
**Ngày tạo**: 10/02/2026
