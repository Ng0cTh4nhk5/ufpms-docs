# DFD Cấp 2 - Chi Tiết Quy Trình Phê Duyệt

> 📊 **Cấp**: 2 (Phân rã Quy trình Chi tiết)  
> 🎯 **Phạm vi**: Phân rã mô-đun Quy trình Phê duyệt  
> 📅 **Ngày tạo**: 11/02/2026

---

## 📊 Biểu đồ Luồng Dữ Liệu Cấp 2

```mermaid
flowchart TD
    subgraph External["Thực Thể Bên Ngoài"]
        RES[Nhà Nghiên Cứu]
        FCR[Người Đánh Giá Cấp Khoa]
        UNR[Người Đánh Giá Cấp Trường]
    end
    
    subgraph Level_2_Processes["2.0 Quy Trình Phê Duyệt - Quy Trình Chi Tiết"]
        P21["2.1<br/>Xác Thực<br/>Bài Gửi"]
        P22["2.2<br/>Phân Công<br/>Người Đánh Giá Khoa"]
        P23["2.3<br/>Đánh Giá<br/>Cấp Khoa"]
        P24["2.4<br/>Đánh Giá<br/>Cấp Trường"]
        P25["2.5<br/>Cập Nhật<br/>Trạng Thái Ấn Phẩm"]
        P26["2.6<br/>Gửi<br/>Thông Báo"]
        P27["2.7<br/>Ghi Nhật Ký<br/>Lịch Sử"]
    end
    
    subgraph DataStores["Kho Dữ Liệu"]
        D1[(D1: Ấn Phẩm)]
        D2[(D2: Người Dùng)]
        D3[(D3: Lịch Sử Đánh Giá)]
        D4[(D4: Bình Luận Đánh Giá)]
    end
    
    %% Luồng từ Bên ngoài đến Quy trình
    RES -->|Yêu cầu gửi| P21
    FCR -->|Quyết định đánh giá| P23
    UNR -->|Quyết định phê duyệt| P24
    
    %% Luồng từ Quy trình đến Bên ngoài
    P26 -->|Email đã nhận bài gửi| RES
    P26 -->|Email phân công đánh giá| FCR
    P26 -->|Email cập nhật trạng thái| RES
    P26 -->|Email phê duyệt cuối cùng| RES
    
    %% Luồng từ Quy trình đến Kho Dữ liệu
    P21 <-->|Đọc ấn phẩm| D1
    P22 -->|Đọc người đánh giá theo khoa| D2
    P23 <-->|Đọc ấn phẩm| D1
    P24 <-->|Đọc ấn phẩm| D1
    P25 -->|Ghi cập nhật trạng thái| D1
    P26 <-->|Đọc email người dùng| D2
    P27 -->|Ghi bản ghi lịch sử| D3
    P23 -->|Ghi bình luận| D4
    P24 -->|Ghi bình luận| D4
    
    %% Luồng giữa các Quy trình
    P21 -->|Bài gửi hợp lệ| P22
    P22 -->|Người đánh giá đã phân công| P23
    P23 -->|Khoa đã phê duyệt| P24
    P23 -->|Yêu cầu chỉnh sửa| P25
    P23 -->|Đã từ chối| P25
    P24 -->|Trường đã phê duyệt| P25
    P24 -->|Gửi lại| P22
    P25 -->|Trạng thái đã đổi| P26
    P25 -->|Trạng thái đã đổi| P27
    
    style P21 fill:#ffccbc
    style P22 fill:#ffab91
    style P23 fill:#ff8a65
    style P24 fill:#ff7043
    style P25 fill:#ff6b9d
    style P26 fill:#ffcdd2
    style P27 fill:#f8bbd0
```

---

## 📋 Đặc Tả Quy Trình Chi Tiết

### 2.1 Xác Thực Bài Gửi

**Đầu vào**:
- Yêu cầu gửi (từ Nhà nghiên cứu)
- Dữ liệu ấn phẩm (từ D1)

**Quy trình**:
1. Kiểm tra trạng thái ấn phẩm = DRAFT
2. Kiểm tra quyền sở hữu (người gửi = chủ sở hữu)
3. Xác thực các trường bắt buộc:
   - Tiêu đề đã điền
   - Ít nhất 1 tác giả
   - PDF đã tải lên
4. Kiểm tra trùng lặp DOI (nếu được cung cấp)

**Đầu ra**:
- Bài gửi hợp lệ → đến 2.2
- Bài gửi không hợp lệ → thông báo lỗi cho Nhà nghiên cứu

**Truy Cập Kho Dữ Liệu**:
- ĐỌC: D1 (Ấn Phẩm)

---

### 2.2 Phân Công Người Đánh Giá Cấp Khoa

**Đầu vào**:
- Bài gửi hợp lệ (từ 2.1)

**Quy trình**:
1. Lấy khoa của nhà nghiên cứu
2. Truy vấn người đánh giá khoa đang hoạt động
3. Chọn người đánh giá (quay vòng P2, thủ công P0)
4. Cập nhật ấn phẩm với phân công người đánh giá

**Đầu ra**:
- Thông tin người đánh giá được phân công → đến 2.3
- Kích hoạt thông báo người đánh giá → đến 2.6

**Truy Cập Kho Dữ Liệu**:
- ĐỌC: D2 (Người dùng - lấy người đánh giá)
- GHI: D1 (Ấn phẩm - phân công người đánh giá)

**Quy Tắc Nghiệp Vụ**:
- Người đánh giá phải thuộc cùng khoa
- Người đánh giá không thể đánh giá ấn phẩm của chính mình

---

### 2.3 Đánh Giá Cấp Khoa

**Đầu vào**:
- Quyết định đánh giá (từ Người Đánh Giá Cấp Khoa)
- Dữ liệu ấn phẩm (từ D1)

**Quy trình**:
1. Xác thực ủy quyền người đánh giá
2. Xử lý quyết định:
   - **Phê duyệt**: Đặt trạng thái = FACULTY_APPROVED → đến 2.4
   - **Yêu cầu Chỉnh sửa**: Đặt trạng thái = REVISION_REQUIRED → đến 2.5
   - **Từ chối**: Đặt trạng thái = REJECTED → đến 2.5
3. Lưu bình luận (nếu có)

**Đầu ra**:
- Đã phê duyệt → đến 2.4 (Đánh Giá Cấp Trường)
- Chỉnh sửa/Từ chối → đến 2.5 (Cập Nhật Trạng Thái)

**Truy Cập Kho Dữ Liệu**:
- ĐỌC: D1 (Ấn Phẩm)
- GHI: D4 (Bình Luận Đánh Giá)

---

### 2.4 Đánh Giá Cấp Trường

**Đầu vào**:
- Quyết định phê duyệt (từ Người Đánh Giá Cấp Trường)
- Dữ liệu ấn phẩm (từ D1)

**Quy trình**:
1. Xác thực ủy quyền người đánh giá (vai trò Người Đánh Giá Cấp Trường)
2. Xử lý quyết định:
   - **Phê duyệt**: Đặt trạng thái = PUBLISHED → đến 2.5
   - **Gửi Lại**: Đặt trạng thái = FACULTY_REVIEWING → đến 2.2

**Đầu ra**:
- Phê duyệt/Gửi Lại → đến 2.5 (Cập Nhật Trạng Thái)

**Truy Cập Kho Dữ Liệu**:
- ĐỌC: D1 (Ấn Phẩm)
- GHI: D4 (Bình Luận Đánh Giá)

**Quy Tắc Nghiệp Vụ**:
- Chỉ Người Đánh Giá Cấp Trường mới có thể xuất bản
- Ấn phẩm đã xuất bản không thể được chỉnh sửa bởi nhà nghiên cứu

---

### 2.5 Cập Nhật Trạng Thái Ấn Phẩm

**Đầu vào**:
- Thay đổi trạng thái (từ 2.3 hoặc 2.4)
- Giá trị trạng thái mới
- Giá trị trạng thái cũ

**Quy trình**:
1. Cập nhật bảng publications (đặt trạng thái, dấu thời gian)
2. Nếu PUBLISHED: đặt published_at = NOW()

**Đầu ra**:
- Trạng thái đã cập nhật → kích hoạt đến 2.6, 2.7

**Truy Cập Kho Dữ Liệu**:
- GHI: D1 (Ấn Phẩm)

**Giao dịch**: Phải nguyên tử (atomic)

---

### 2.6 Gửi Thông Báo

**Đầu vào**:
- Sự kiện thay đổi trạng thái (từ 2.5)
- Dữ liệu người dùng (từ D2)

**Quy trình**:
1. Xác định người nhận dựa trên sự kiện:
   - SUBMITTED → Người đánh giá khoa
   - FACULTY_APPROVED → Nhà nghiên cứu (chủ sở hữu)
   - REVISION_REQUIRED → Nhà nghiên cứu
   - REJECTED → Nhà nghiên cứu
   - PUBLISHED → Nhà nghiên cứu + đồng tác giả
2. Soạn email từ mẫu
3. Gửi qua Máy chủ Email (bên ngoài)

**Đầu ra**:
- Email đã gửi đến người nhận

**Truy Cập Kho Dữ Liệu**:
- ĐỌC: D2 (Người dùng - lấy email)

**Không đồng bộ**: Gửi email nên không đồng bộ (hàng đợi)

---

### 2.7 Ghi Nhật Ký Lịch Sử

**Đầu vào**:
- Sự kiện thay đổi trạng thái (từ 2.5)
- Tác nhân (người đánh giá/nhà nghiên cứu)
- Bình luận (nếu có)

**Quy trình**:
1. Tạo bản ghi lịch sử:
   - từ_trạng_thái
   - đến_trạng_thái
   - id_tác_nhân
   - hành_động
   - dấu_thời_gian

**Đầu ra**:
- Bản ghi lịch sử đã lưu

**Truy Cập Kho Dữ Liệu**:
- GHI: D3 (Lịch Sử Đánh Giá)

**Kiểm toán**: Bản ghi bất biến để tuân thủ

---

## 🔄 Chuyển Đổi Trạng Thái Quy Trình

```mermaid
stateDiagram-v2
    [*] --> DRAFT: Tạo
    DRAFT --> SUBMITTED: 2.1 Xác thực
    SUBMITTED --> FACULTY_REVIEWING: 2.2 Phân công
    
    FACULTY_REVIEWING --> FACULTY_APPROVED: 2.3 Phê duyệt
    FACULTY_REVIEWING --> REVISION_REQUIRED: 2.3 Yêu cầu Chỉnh sửa
    FACULTY_REVIEWING --> REJECTED: 2.3 Từ chối
    
    REVISION_REQUIRED --> DRAFT: Nhà nghiên cứu chỉnh sửa
    
    FACULTY_APPROVED --> UNIVERSITY_REVIEWING: 2.4 Tự động chuyển đổi
    
    UNIVERSITY_REVIEWING --> PUBLISHED: 2.4 Phê duyệt
    UNIVERSITY_REVIEWING --> FACULTY_REVIEWING: 2.4 Gửi lại
    
    PUBLISHED --> [*]
    REJECTED --> [*]
```

---

## 📊 Chi Tiết Kho Dữ Liệu

### D1: Ấn Phẩm
**Được truy cập bởi**: 2.1, 2.2, 2.3, 2.4, 2.5  
**Thao tác**: ĐỌC, GHI (cập nhật trạng thái)

### D2: Người Dùng
**Được truy cập bởi**: 2.2, 2.6  
**Thao tác**: CHỈ ĐỌC (lấy người đánh giá, lấy email)

### D3: Lịch Sử Đánh Giá
**Được truy cập bởi**: 2.7  
**Thao tác**: CHỈ GHI (nhật ký kiểm toán chỉ thêm)

### D4: Bình Luận Đánh Giá
**Được truy cập bởi**: 2.3, 2.4  
**Thao tác**: GHI (chèn bình luận)

---

## ⏱️ Thời Gian Quy Trình

| Quy Trình | Thời Lượng TB | Loại |
|-----------|---------------|------|
| 2.1 Xác thực | < 1 giây | Đồng bộ |
| 2.2 Phân công | < 2 giây | Đồng bộ |
| 2.3 Đánh Giá Cấp Khoa | 3-7 ngày | Quyết định con người |
| 2.4 Đánh Giá Cấp Trường | 3-7 ngày | Quyết định con người |
| 2.5 Cập Nhật Trạng Thái | < 1 giây | Đồng bộ |
| 2.6 Thông báo | 2-5 giây | Không đồng bộ |
| 2.7 Ghi Lịch Sử | < 1 giây | Đồng bộ |

**Tổng SLA**: 6-14 ngày (DRAFT → PUBLISHED)

---

**Liên quan**: act_approval_workflow.md, seq_faculty_review.md, seq_university_approval.md  
**Ngày tạo**: 11/02/2026
