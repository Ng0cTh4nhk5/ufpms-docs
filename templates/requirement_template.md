# Requirement Template

## Requirement ID: REQ-XXX

---

## Thông Tin Cơ Bản

| Thuộc tính | Giá trị |
|------------|---------|
| **ID** | REQ-XXX |
| **Type** | Functional / Non-Functional |
| **Category** | [Ví dụ: User Management, Security, Performance] |
| **Priority** | High / Medium / Low |
| **Status** | Draft / Approved / Implemented / Verified |
| **Created By** | [Tên người tạo] |
| **Created Date** | [DD/MM/YYYY] |
| **Last Updated** | [DD/MM/YYYY] |

---

## Requirement Statement

**Hệ thống phải** [mô tả yêu cầu một cách rõ ràng, ngắn gọn]

---

## Detailed Description

[Mô tả chi tiết yêu cầu, bao gồm context, rationale, và expected behavior]

### Context
[Bối cảnh sử dụng yêu cầu này]

### Rationale
[Lý do tại sao yêu cầu này cần thiết]

### Expected Behavior
[Hành vi mong đợi của hệ thống]

---

## Acceptance Criteria

### Criterion 1
- **Given**: [Điều kiện]
- **When**: [Hành động]
- **Then**: [Kết quả]

### Criterion 2
- **Given**: [Điều kiện]
- **When**: [Hành động]
- **Then**: [Kết quả]

---

## Fit Criterion (Đo lường)

[Cách đo lường để xác định yêu cầu đã được thỏa mãn]

**Ví dụ cho yêu cầu phi chức năng:**
- Performance: Response time < 2 seconds for 95% of requests
- Security: All passwords must be hashed using bcrypt
- Usability: 90% of users can complete task without help

---

## Dependencies

### Prerequisites
- [REQ-YYY]: [Yêu cầu cần hoàn thành trước]
- [REQ-ZZZ]: [Yêu cầu cần hoàn thành trước]

### Related Requirements
- [REQ-AAA]: [Yêu cầu liên quan]
- [REQ-BBB]: [Yêu cầu liên quan]

---

## Constraints

- [Ràng buộc 1: Ví dụ - Must use existing authentication system]
- [Ràng buộc 2: Ví dụ - Must comply with GDPR]
- [Ràng buộc 3]

---

## Assumptions

- [Giả định 1: Ví dụ - Users have modern web browsers]
- [Giả định 2: Ví dụ - Internet connection available]
- [Giả định 3]

---

## Related Artifacts

### Use Cases
- [UC-XXX]: [Tên use case]

### User Stories
- [US-XXX]: [Tên user story]

### Design Documents
- [Link đến design document nếu có]

### Test Cases
- [TC-XXX]: [Tên test case]

---

## Implementation Notes

### Technical Approach
[Gợi ý về cách implement]

### Potential Challenges
- [Challenge 1]
- [Challenge 2]

### Suggested Solutions
- [Solution 1]
- [Solution 2]

---

## Verification Method

- [ ] Inspection - Review code/design
- [ ] Analysis - Static analysis
- [ ] Testing - Unit/Integration/System tests
- [ ] Demonstration - Show working feature

**Test Scenarios:**
1. [Scenario 1]
2. [Scenario 2]

---

## Non-Functional Attributes (Nếu áp dụng)

### Performance
- Response time: [Giá trị]
- Throughput: [Giá trị]

### Security
- Authentication: [Yêu cầu]
- Authorization: [Yêu cầu]
- Data encryption: [Yêu cầu]

### Usability
- Learning time: [Thời gian]
- Error rate: [Tỷ lệ]

### Reliability
- MTBF (Mean Time Between Failures): [Giá trị]
- Availability: [%]

### Scalability
- Concurrent users: [Số lượng]
- Data volume: [Kích thước]

---

## Notes

[Ghi chú bổ sung, quyết định đã đưa ra, câu hỏi còn tồn đọng]

---

## Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | [DD/MM/YYYY] | [Tên] | Initial draft |
| 1.1 | [DD/MM/YYYY] | [Tên] | [Mô tả thay đổi] |

---

## Approval

| Role | Name | Signature | Date |
|------|------|-----------|------|
| Product Owner | | | |
| Technical Lead | | | |
| QA Lead | | | |
