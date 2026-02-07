# Use Case Template - Chi Tiết

## Use Case ID: UC-XXX

### Use Case Name
[Tên đầy đủ của use case]

---

## Metadata

| Thuộc tính | Giá trị |
|------------|---------|
| **Use Case ID** | UC-XXX |
| **Created By** | [Tên người tạo] |
| **Date Created** | [DD/MM/YYYY] |
| **Last Updated** | [DD/MM/YYYY] |
| **Version** | 1.0 |

---

## Brief Description

[Mô tả ngắn gọn 2-3 câu về use case này]

---

## Actors

### Primary Actor
- [Actor chính - người khởi tạo use case]

### Secondary Actors
- [Actor phụ 1]
- [Actor phụ 2]

---

## Preconditions

- [ ] Điều kiện 1 phải được thỏa mãn trước khi use case bắt đầu
- [ ] Điều kiện 2 phải được thỏa mãn trước khi use case bắt đầu
- [ ] Điều kiện 3...

---

## Postconditions

### Success End Condition
- [Trạng thái hệ thống sau khi use case thành công]

### Failure End Condition
- [Trạng thái hệ thống nếu use case thất bại]

---

## Main Flow (Basic Flow)

| Bước | Actor | Hệ Thống |
|------|-------|----------|
| 1 | [Actor] thực hiện hành động... | |
| 2 | | Hệ thống xác thực... |
| 3 | | Hệ thống hiển thị... |
| 4 | [Actor] nhập thông tin... | |
| 5 | | Hệ thống xử lý... |
| 6 | | Hệ thống lưu dữ liệu... |
| 7 | | Hệ thống hiển thị thông báo thành công |

---

## Alternative Flows

### Alt-1: [Tên luồng thay thế 1]

**Trigger**: At step X, [điều kiện kích hoạt]

| Bước | Mô tả |
|------|-------|
| X.1 | [Bước xử lý thay thế] |
| X.2 | [Bước xử lý thay thế] |
| X.3 | Resume at step Y of Main Flow |

### Alt-2: [Tên luồng thay thế 2]

**Trigger**: At step Y, [điều kiện kích hoạt]

| Bước | Mô tả |
|------|-------|
| Y.1 | [Bước xử lý thay thế] |
| Y.2 | [Bước xử lý thay thế] |
| Y.3 | Use case ends |

---

## Exception Flows

### Exc-1: [Tên ngoại lệ 1]

**Trigger**: At step X, [điều kiện lỗi]

| Bước | Mô tả |
|------|-------|
| X.E1 | Hệ thống hiển thị thông báo lỗi |
| X.E2 | [Xử lý lỗi] |
| X.E3 | Use case ends / Resume at step Z |

### Exc-2: [Tên ngoại lệ 2]

**Trigger**: At step Y, [điều kiện lỗi]

| Bước | Mô tả |
|------|-------|
| Y.E1 | Hệ thống ghi log lỗi |
| Y.E2 | Hệ thống rollback transaction |
| Y.E3 | Use case ends |

---

## Business Rules

| ID | Business Rule |
|----|---------------|
| BR-1 | [Quy tắc nghiệp vụ 1] |
| BR-2 | [Quy tắc nghiệp vụ 2] |
| BR-3 | [Quy tắc nghiệp vụ 3] |

---

## Special Requirements

### Non-Functional Requirements
- **Performance**: [Ví dụ: Thời gian phản hồi < 2 giây]
- **Security**: [Ví dụ: Yêu cầu HTTPS, mã hóa dữ liệu]
- **Usability**: [Ví dụ: Giao diện responsive]
- **Reliability**: [Ví dụ: 99.9% uptime]

### Technical Constraints
- [Ràng buộc kỹ thuật 1]
- [Ràng buộc kỹ thuật 2]

---

## UI Requirements

### Screen Mockups
- [Link hoặc nhúng ảnh mockup]

### Input Fields

| Field Name | Type | Required | Validation Rules |
|------------|------|----------|------------------|
| [Tên trường] | [Text/Number/Date...] | Yes/No | [Quy tắc validate] |
| [Tên trường] | [Type] | Yes/No | [Quy tắc validate] |

### Output Display
- [Mô tả thông tin hiển thị]
- [Format hiển thị]

---

## Data Elements

### Input Data
- [Dữ liệu đầu vào 1]: [Mô tả]
- [Dữ liệu đầu vào 2]: [Mô tả]

### Output Data
- [Dữ liệu đầu ra 1]: [Mô tả]
- [Dữ liệu đầu ra 2]: [Mô tả]

---

## Related Use Cases

### Includes
- [UC-YYY]: [Tên use case được include]

### Extends
- [UC-ZZZ]: [Tên use case mở rộng]

### Related
- [UC-AAA]: [Tên use case liên quan]

---

## Related User Stories
- US-XXX: [Tên user story]
- US-YYY: [Tên user story]

---

## Diagrams

### Sequence Diagram
- [Link đến sequence diagram: seq_uc_xxx.drawio]

### Activity Diagram
- [Link đến activity diagram: act_uc_xxx.drawio]

---

## Notes and Issues

### Open Issues
- [ ] Issue 1: [Mô tả vấn đề chưa giải quyết]
- [ ] Issue 2: [Mô tả vấn đề chưa giải quyết]

### Additional Notes
- [Ghi chú bổ sung]
- [Decisions made]
- [Assumptions]

---

## Revision History

| Version | Date | Author | Description |
|---------|------|--------|-------------|
| 1.0 | [DD/MM/YYYY] | [Tên] | Initial version |
| 1.1 | [DD/MM/YYYY] | [Tên] | [Mô tả thay đổi] |
