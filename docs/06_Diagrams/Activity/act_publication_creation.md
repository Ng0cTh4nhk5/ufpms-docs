# Quy Trình Tạo Ấn Phẩm - Biểu đồ Hoạt động

> 📊 **Biểu đồ**: Tạo Ấn phẩm  
> 🎯 **Phạm vi**: Tạo và lưu ấn phẩm  
> 👤 **Tác nhân**: Nhà nghiên cứu

---

## 📊 Biểu đồ Hoạt động

```mermaid
flowchart TD
    Start(["Nhà nghiên cứu nhấn Tạo Ấn phẩm"]) --> LoadForm["Tải biểu mẫu tạo mới"]
    
    LoadForm --> GetMetadata["Lấy tùy chọn siêu dữ liệu từ cơ sở dữ liệu"]
    GetMetadata --> DisplayForm["Hiển thị biểu mẫu trống"]
    
    DisplayForm --> FillBasic{"Điền thông tin cơ bản?"}
    
    FillBasic -->|"Nhập dữ liệu"| EnterTitle["Nhập tiêu đề"]
    EnterTitle --> EnterJournal["Nhập tạp chí/hội nghị"]
    EnterJournal --> EnterYear["Nhập năm"]
    EnterYear --> SelectType["Chọn loại ấn phẩm"]
    SelectType --> EnterDOI["Nhập DOI (tùy chọn)"]
    
    EnterDOI --> FillAuthors{"Thêm tác giả?"}
    
    FillAuthors -->|"Có"| AddAuthor["Thêm tác giả: tên, thứ tự, đơn vị"]
    AddAuthor --> MoreAuthors{"Thêm tác giả khác?"}
    MoreAuthors -->|"Có"| AddAuthor
    MoreAuthors -->|"Không"| FillAbstract
    
    FillAuthors -->|"Bỏ qua"| FillAbstract["Nhập tóm tắt (tùy chọn)"]
    
    FillAbstract --> FillKeywords["Nhập từ khóa (tùy chọn)"]
    
    FillKeywords --> UploadPDF{"Tải lên PDF?"}
    
    UploadPDF -->|"Có"| SelectFile["Chọn tệp PDF"]
    SelectFile --> ValidateFile{"Tệp hợp lệ?"}
    
    ValidateFile -->|"Không: >10MB hoặc không phải PDF"| ShowError1["Hiển thị thông báo lỗi"]
    ShowError1 --> SelectFile
    
    ValidateFile -->|"Có"| UploadFile["Tải lên máy chủ"]
    UploadFile --> SavePath["Lưu đường dẫn tệp"]
    SavePath --> Decision
    
    UploadPDF -->|"Không"| Decision{"Hành động?"}
    
    Decision -->|"Lưu nháp"| ValidateDraft{"Các trường bắt buộc đã điền?"}
    
    ValidateDraft -->|"Không: Thiếu tiêu đề"| ShowError2["Hiển thị lỗi xác thực"]
    ShowError2 --> EnterTitle
    
    ValidateDraft -->|"Có"| CheckDuplicate["Kiểm tra trùng lặp DOI nếu được cung cấp"]
    
    CheckDuplicate -->|"Tìm thấy trùng lặp"| ShowError3["Hiển thị lỗi: DOI đã tồn tại"]
    ShowError3 --> EnterDOI
    
    CheckDuplicate -->|"Không trùng lặp"| SaveDraft["Lưu vào cơ sở dữ liệu - Trạng thái: DRAFT"]
    SaveDraft --> Success1["Hiển thị thông báo thành công"]
    Success1 --> End1(["Chuyển hướng đến Ấn phẩm của tôi"])
    
    Decision -->|"Hủy"| Confirm{"Xác nhận hủy?"}
    Confirm -->|"Có"| End2(["Quay lại bảng điều khiển"])
    Confirm -->|"Không"| DisplayForm
    
    style Start fill:#e3f2fd
    style End1 fill:#c8e6c9
    style End2 fill:#ffccbc
    style SaveDraft fill:#fff9c4
    style ShowError1 fill:#ffcdd2
    style ShowError2 fill:#ffcdd2
    style ShowError3 fill:#ffcdd2
```

---

## 📋 Chi Tiết Các Bước

### 1. Tải Biểu Mẫu
- Lấy danh sách loại ấn phẩm (Tạp chí, Hội nghị, Chương sách, v.v.)
- Lấy danh sách lĩnh vực nghiên cứu
- Hiển thị biểu mẫu trống

### 2. Điền Thông Tin Cơ Bản
**Bắt buộc**:
- Tiêu đề (tối thiểu 10 ký tự)

**Tùy chọn nhưng quan trọng**:
- Tên Tạp chí/Hội nghị
- Năm (1900-năm hiện tại)
- Loại ấn phẩm
- DOI
- ISSN

### 3. Thêm Tác Giả
- Nhà nghiên cứu (chủ sở hữu) tự động được thêm là tác giả đầu tiên
- Có thể thêm đồng tác giả:
  - Tên
  - Thứ tự (1, 2, 3...)
  - Đơn vị công tác
  - Hộp kiểm tác giả liên hệ

### 4. Thông Tin Bổ Sung
- Tóm tắt (khuyến nghị, tối thiểu 100 ký tự)
- Từ khóa (phân tách bằng dấu phẩy)
- URL (tùy chọn)

### 5. Tải Lên PDF
- Kích thước tệp: tối đa 10MB
- Định dạng: chỉ PDF
- Xác thực trên máy khách + máy chủ

### 6. Lưu Nháp
**Xác thực**:
- Yêu cầu tiêu đề
- Ít nhất 1 tác giả (chủ sở hữu)
- Kiểm tra tính duy nhất của DOI (nếu được cung cấp)

**Cơ sở dữ liệu**:
- INSERT vào publications (trạng thái = DRAFT)
- INSERT vào publication_authors
- Đặt created_at = now()

---

## ⏱️ Thời Gian Trung Bình

- Nháp nhanh (chỉ tiêu đề): ~30 giây
- Thông tin đầy đủ (không có PDF): ~3-5 phút
- Ấn phẩm đầy đủ (có PDF): ~5-10 phút

---

## 🚨 Các Tình Huống Lỗi

### 1. Lỗi Xác Thực
- Tiêu đề quá ngắn
- Năm không hợp lệ
- Định dạng URL không hợp lệ

### 2. Lỗi Tải Tệp
- Tệp quá lớn (>10MB)
- Không phải tệp PDF
- Tải lên thất bại (lỗi mạng)

### 3. Trùng Lặp DOI
- DOI đã tồn tại trong hệ thống
- Người dùng phải thay đổi DOI hoặc liên hệ quản trị viên

---

## 💡 Quy Tắc Nghiệp Vụ

1. **Tự động lưu** (P1): Bản nháp tự động lưu mỗi 60 giây
2. **PDF sau**: Có thể lưu nháp mà không cần PDF, tải lên sau
3. **Chỉnh sửa bất cứ lúc nào**: Có thể chỉnh sửa ấn phẩm DRAFT (Nháp)
4. **Yêu cầu khi gửi**: Cần có PDF + thông tin đầy đủ trước khi gửi

---

**Liên quan**: UC-D1-01, seq_create_publication.md  
**Ngày tạo**: 11/02/2026
