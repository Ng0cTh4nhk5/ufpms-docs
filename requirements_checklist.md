# Checklist Đặc Tả và Phân Tích Hệ Thống

## 1. Xác Định Đặc Tả Hệ Thống (System Specification)

### 1.1. Thông Tin Tổng Quan
- [ ] Tên hệ thống
- [ ] Mục đích và phạm vi của hệ thống
- [ ] Các bên liên quan (stakeholders)
- [ ] Môi trường triển khai (deployment environment)
- [ ] Công nghệ và nền tảng sử dụng

### 1.2. Ranh Giới Hệ Thống
- [ ] Xác định các chức năng nằm trong phạm vi hệ thống
- [ ] Xác định các chức năng nằm ngoài phạm vi hệ thống
- [ ] Các hệ thống/dịch vụ bên ngoài cần tích hợp

### 1.3. Ràng Buộc và Giả Định
- [ ] Ràng buộc về công nghệ
- [ ] Ràng buộc về thời gian và ngân sách
- [ ] Ràng buộc về quy định pháp luật
- [ ] Các giả định về người dùng và môi trường

---

## 2. Làm Rõ Hệ Thống (System Clarification)

### 2.1. Bối Cảnh Nghiệp Vụ
- [ ] Mô tả quy trình nghiệp vụ hiện tại (as-is)
- [ ] Xác định vấn đề cần giải quyết
- [ ] Mô tả quy trình nghiệp vụ tương lai (to-be)
- [ ] Lợi ích mong đợi từ hệ thống

### 2.2. Phân Tích Người Dùng
- [ ] Xác định các nhóm người dùng (user groups)
- [ ] Đặc điểm của từng nhóm người dùng
- [ ] Kỹ năng và kinh nghiệm công nghệ
- [ ] Nhu cầu và mong đợi của người dùng

### 2.3. Sơ Đồ Ngữ Cảnh
- [ ] Vẽ Context Diagram
- [ ] Xác định các actor bên ngoài
- [ ] Xác định luồng dữ liệu chính

---

## 3. Yêu Cầu Chức Năng (Functional Requirements)

### 3.1. Liệt Kê Chức Năng Chính
- [ ] Chức năng 1: [Mô tả chi tiết]
- [ ] Chức năng 2: [Mô tả chi tiết]
- [ ] Chức năng 3: [Mô tả chi tiết]
- [ ] ...

### 3.2. Đặc Tả Chi Tiết
- [ ] Mô tả đầu vào cho mỗi chức năng
- [ ] Mô tả đầu ra cho mỗi chức năng
- [ ] Quy tắc nghiệp vụ (business rules)
- [ ] Xử lý lỗi và ngoại lệ

### 3.3. Phân Loại Theo Module
- [ ] Module quản lý người dùng
- [ ] Module xử lý nghiệp vụ chính
- [ ] Module báo cáo và thống kê
- [ ] Module tích hợp
- [ ] ...

---

## 4. Yêu Cầu Phi Chức Năng (Non-Functional Requirements)

### 4.1. Hiệu Năng (Performance)
- [ ] Thời gian phản hồi (response time)
- [ ] Throughput (số lượng giao dịch/giây)
- [ ] Số người dùng đồng thời

### 4.2. Bảo Mật (Security)
- [ ] Xác thực và phân quyền
- [ ] Mã hóa dữ liệu
- [ ] Audit log và giám sát
- [ ] Tuân thủ tiêu chuẩn bảo mật

### 4.3. Khả Dụng (Availability)
- [ ] Uptime mong đợi (%)
- [ ] Kế hoạch backup và recovery
- [ ] Redundancy và failover

### 4.4. Khả Năng Mở Rộng (Scalability)
- [ ] Khả năng mở rộng theo chiều ngang
- [ ] Khả năng mở rộng theo chiều dọc
- [ ] Dự kiến tăng trưởng

### 4.5. Tính Khả Dụng (Usability)
- [ ] Giao diện thân thiện
- [ ] Hỗ trợ đa ngôn ngữ
- [ ] Responsive design
- [ ] Accessibility

### 4.6. Khả Năng Bảo Trì (Maintainability)
- [ ] Cấu trúc code rõ ràng
- [ ] Tài liệu kỹ thuật
- [ ] Logging và monitoring

### 4.7. Tương Thích (Compatibility)
- [ ] Trình duyệt được hỗ trợ
- [ ] Thiết bị được hỗ trợ
- [ ] Tích hợp với hệ thống khác

---

## 5. User Stories

### 5.1. Cấu Trúc User Story
- [ ] Xác định template: "Là [vai trò], tôi muốn [chức năng], để [lợi ích]"
- [ ] Định nghĩa Acceptance Criteria cho mỗi story

### 5.2. User Stories Theo Vai Trò

#### 5.2.1. Người Dùng Cuối (End User)
- [ ] Story 1: [Mô tả]
  - Acceptance Criteria:
    - [ ] Tiêu chí 1
    - [ ] Tiêu chí 2
- [ ] Story 2: [Mô tả]
- [ ] ...

#### 5.2.2. Quản Trị Viên (Admin)
- [ ] Story 1: [Mô tả]
  - Acceptance Criteria:
    - [ ] Tiêu chí 1
    - [ ] Tiêu chí 2
- [ ] Story 2: [Mô tả]
- [ ] ...

#### 5.2.3. Các Vai Trò Khác
- [ ] Story 1: [Mô tả]
- [ ] ...

### 5.3. Ưu Tiên User Stories
- [ ] Priority High: [Danh sách stories]
- [ ] Priority Medium: [Danh sách stories]
- [ ] Priority Low: [Danh sách stories]

---

## 6. Use Cases

### 6.1. Use Case Tổng Quát (High-Level)

#### 6.1.1. Use Case Diagram Tổng Quan
- [ ] Vẽ Use Case Diagram tổng quan
- [ ] Xác định tất cả actors
- [ ] Xác định các use case chính
- [ ] Xác định mối quan hệ giữa actors và use cases

#### 6.1.2. Danh Sách Use Case Level 0
- [ ] UC-001: [Tên use case - mức tổng quát]
- [ ] UC-002: [Tên use case - mức tổng quát]
- [ ] UC-003: [Tên use case - mức tổng quát]
- [ ] ...

### 6.2. Use Case Mức Trung Bình (Medium-Level)

#### 6.2.1. Mở Rộng Use Case Điển Hình
Cho mỗi use case cấp cao, tạo đặc tả chi tiết hơn:

- [ ] **UC-001: [Tên]**
  - Brief Description: [Mô tả ngắn gọn]
  - Actors: [Danh sách actors]
  - Preconditions: [Điều kiện trước]
  - Postconditions: [Điều kiện sau]
  - Main Flow: [Luồng chính - các bước tổng quát]
  - Alternative Flows: [Các luồng thay thế]

- [ ] **UC-002: [Tên]**
  - [Tương tự như trên]

### 6.3. Use Case Chi Tiết (Detailed-Level)

#### 6.3.1. Đặc Tả Use Case Đầy Đủ

Cho mỗi use case quan trọng, tạo đặc tả đầy đủ:

- [ ] **UC-001-Detail: [Tên]**
  - **Use Case ID**: UC-001
  - **Use Case Name**: [Tên đầy đủ]
  - **Created By**: [Tên người tạo]
  - **Date Created**: [Ngày tạo]
  - **Last Updated**: [Ngày cập nhật]
  
  - **Brief Description**: 
    - [Mô tả 2-3 câu về use case]
  
  - **Actors**: 
    - Primary: [Actor chính]
    - Secondary: [Actor phụ]
  
  - **Preconditions**: 
    - [ ] Điều kiện 1
    - [ ] Điều kiện 2
  
  - **Postconditions**: 
    - Success: [Kết quả khi thành công]
    - Failure: [Kết quả khi thất bại]
  
  - **Main Flow**:
    1. [Actor] thực hiện hành động...
    2. Hệ thống xử lý...
    3. Hệ thống hiển thị...
    4. [Actor] nhập...
    5. ...
  
  - **Alternative Flows**:
    - **Alt-1: [Tên luồng thay thế]**
      - At step X: [Điều kiện kích hoạt]
      - X.1. [Bước xử lý]
      - X.2. ...
      - Resume at step Y
    
    - **Alt-2: [Tên luồng thay thế khác]**
      - [Tương tự]
  
  - **Exception Flows**:
    - **Exc-1: [Tên ngoại lệ]**
      - At step X: [Điều kiện lỗi]
      - X.1. [Xử lý lỗi]
      - X.2. Use case ends
  
  - **Business Rules**:
    - BR-1: [Quy tắc nghiệp vụ]
    - BR-2: [Quy tắc nghiệp vụ]
  
  - **Special Requirements**:
    - [ ] Yêu cầu phi chức năng liên quan
    - [ ] Ràng buộc kỹ thuật
  
  - **UI Requirements**:
    - [ ] Mockup/wireframe
    - [ ] Các trường dữ liệu cần hiển thị
    - [ ] Validation rules
  
  - **Notes and Issues**:
    - [Các ghi chú bổ sung]

- [ ] **UC-002-Detail: [Tên]**
  - [Đặc tả đầy đủ tương tự]

- [ ] **UC-003-Detail: [Tên]**
  - [Đặc tả đầy đủ tương tự]

#### 6.3.2. Sequence Diagrams
- [ ] Vẽ Sequence Diagram cho UC-001
- [ ] Vẽ Sequence Diagram cho UC-002
- [ ] Vẽ Sequence Diagram cho UC-003
- [ ] ...

#### 6.3.3. Activity Diagrams
- [ ] Vẽ Activity Diagram cho use case phức tạp 1
- [ ] Vẽ Activity Diagram cho use case phức tạp 2
- [ ] ...

---

## 7. Xác Thực và Phê Duyệt

### 7.1. Review
- [ ] Review với stakeholders
- [ ] Review với đội phát triển
- [ ] Review với đội kiểm thử

### 7.2. Điều Chỉnh
- [ ] Tích hợp feedback
- [ ] Cập nhật tài liệu
- [ ] Versioning

### 7.3. Phê Duyệt
- [ ] Xác nhận từ Product Owner
- [ ] Xác nhận từ Technical Lead
- [ ] Phê duyệt chính thức

---

## 8. Tài Liệu Hóa

### 8.1. Tài Liệu Yêu Cầu
- [ ] Software Requirements Specification (SRS)
- [ ] Use Case Specification Document
- [ ] User Stories Document

### 8.2. Sơ Đồ
- [ ] Context Diagram
- [ ] Use Case Diagrams
- [ ] Sequence Diagrams
- [ ] Activity Diagrams
- [ ] Data Flow Diagrams (nếu cần)

### 8.3. Traceability Matrix
- [ ] Tạo bảng liên kết giữa requirements, user stories, và use cases
- [ ] Đảm bảo mọi requirement đều có use case tương ứng

---

## Ghi Chú Sử Dụng

1. **Tiến độ**: Đánh dấu `[x]` khi hoàn thành mục
2. **Linh hoạt**: Điều chỉnh checklist phù hợp với dự án cụ thể
3. **Ưu tiên**: Tập trung vào các mục quan trọng nhất trước
4. **Lặp lại**: Quá trình có thể lặp lại và cải tiến liên tục
