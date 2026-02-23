# BA Deliverable 6: Assumptions Log & Decisions

> 📋 **Phiên bản**: V1.0  
> 👤 **Vai trò**: Business Analyst  
> 📅 **Ngày tạo**: 20/02/2026  
> 🎯 **Mục đích**: Ghi nhận các giả định và quyết định quan trọng trong quá trình phân tích

---

## Tổng Quan

Tài liệu này ghi lại các **giả định (assumptions)** được đưa ra trong quá trình phân tích và thiết kế Phase 1. Mỗi giả định cần được xác nhận với stakeholder hoặc người có thẩm quyền.

---

## Assumptions (Giả Định)

### A-001: Ngôn ngữ giao diện
- **Giả định**: Giao diện bằng tiếng Việt, fallback một số label kỹ thuật bằng tiếng Anh
- **Lý do**: Người dùng chính là giảng viên Việt Nam
- **Trạng thái**: ✅ Đã xác nhận (theo SOP)
- **Ảnh hưởng**: UI labels, error messages, validation messages đều bằng tiếng Việt

---

### A-002: Trình duyệt được hỗ trợ
- **Giả định**: Chrome là primary browser cho V1.0; Firefox và Edge hỗ trợ cơ bản; Mobile không được test
- **Lý do**: Đơn giản hóa scope testing cho V1.0
- **Trạng thái**: ⚠️ Chờ xác nhận stakeholder
- **Ảnh hưởng**: PDF viewer (iframe) có thể hoạt động khác nhau trên các browser

---

### A-003: PDF Viewer inline vs Download
- **Giả định**: Nếu PDF > 10MB, hiển thị **download link** thay vì inline iframe viewer
- **Lý do**: Tránh browser hang khi load file lớn trong iframe
- **Trạng thái**: ⚠️ Chờ xác nhận Dev Lead
- **Ảnh hưởng**: SCR-006 (Publication Detail), US-RES-008

---

### A-004: Co-author giới hạn số lượng
- **Giả định**: Không giới hạn số co-authors trong V1.0
- **Lý do**: Chưa có business requirement cụ thể về giới hạn
- **Trạng thái**: ⚠️ Chờ xác nhận stakeholder
- **Ảnh hưởng**: US-RES-006, Database schema

---

### A-005: Co-author và giờ làm
- **Giả định**: Khi user là co-author của publication PUBLISHED, toàn bộ giờ làm quy đổi vẫn được tính vào dashboard của user đó (không chia theo số tác giả)
- **Lý do**: Quy tắc nhà trường thường tính giờ cho mỗi tác giả độc lập
- **Trạng thái**: ⚠️ **Cần xác nhận gấp** - Ảnh hưởng lớn đến business logic
- **Ảnh hưởng**: US-RES-024, BR-034

---

### A-006: Người dùng biết DOI là gì
- **Giả định**: Users (giảng viên) đã quen với khái niệm DOI, không cần tooltip giải thích
- **Lý do**: Đối tượng người dùng là nghiên cứu viên/giảng viên đại học
- **Trạng thái**: ✅ Chấp nhận cho V1.0
- **Ghi chú**: V2.0 có thể thêm tooltip: "DOI là gì?"

---

### A-007: Upload PDF cho publication đã SUBMITTED
- **Giả định**: Owner có thể upload/update PDF ngay cả khi publication đã SUBMITTED (đang chờ duyệt)
- **Lý do**: Reviewer mới có thể cần xem bản cập nhật
- **Trạng thái**: ⚠️ **Cần xác nhận stakeholder** - Có thể gây confusion cho reviewer
- **Ảnh hưởng**: US-RES-002, SCR-006

---

### A-008: Soft Delete
- **Giả định**: Xóa publication là **soft delete** (đặt `deleted_at`, không xóa row khỏi DB)
- **Lý do**: Hỗ trợ audit trail và khả năng khôi phục trong tương lai
- **Trạng thái**: ✅ Quyết định kỹ thuật (BA + Dev Lead)
- **Ảnh hưởng**: US-RES-004, database schema, API

---

### A-009: Authentication method
- **Giả định**: Sử dụng JWT token, lưu trong localStorage
- **Lý do**: Phổ biến cho SPA, đơn giản cho V1.0
- **Trạng thái**: ✅ Quyết định kỹ thuật (Dev Lead)
- **Ảnh hưởng**: Toàn bộ security layer

---

### A-010: Phân trang (Pagination)
- **Giả định**: Default page size = **10 items/trang** cho Publication List
- **Lý do**: Balance giữa UX và performance
- **Trạng thái**: ✅ Đã quyết định
- **Ảnh hưởng**: SCR-003, API endpoints

---

### A-011: Export Excel format
- **Giả định**: Export file Work Hours Dashboard dưới dạng `.xlsx`
- **Lý do**: Excel phổ biến hơn CSV với người dùng Việt Nam
- **Trạng thái**: ✅ Đã quyết định
- **Ảnh hưởng**: US-RES-024, Backend implementation

---

### A-012: DOI validation
- **Giả định**: DOI validation là **warning**, không phải error - user vẫn có thể save với DOI sai format
- **Lý do**: Một số DOI format cũ có thể không match regex nhưng vẫn hợp lệ
- **Trạng thái**: ⚠️ Chờ xác nhận
- **Ảnh hưởng**: US-RES-001, US-RES-003

---

## Open Questions (Câu Hỏi Chưa Giải Quyết)

| ID | Câu hỏi | Ưu tiên | Deadline | Người trả lời |
|---|---|---|---|---|
| OQ-001 | Upload PDF khi đã SUBMITTED được cho phép không? | 🔴 High | Trước Dev | Stakeholder |
| OQ-002 | Giới hạn số co-authors? | 🟡 Medium | Sprint 1 | Stakeholder/Dev |
| OQ-003 | Co-author có được tính giờ làm? (có thể tính trùng với owner) | 🔴 High | Trước Dev | Stakeholder |
| OQ-004 | PDF viewer threshold (tại bao nhiêu MB thì switch sang download link)? | 🟡 Medium | Sprint 1 | Dev Lead |
| OQ-005 | DOI là warning hay hard error? | 🟡 Medium | Sprint 1 | BA + Dev |

---

## Decisions Log (Quyết Định Đã Xác Nhận)

| ID | Quyết định | Ngày | Do ai | Lý do |
|---|---|---|---|---|
| D-001 | Soft delete cho publications | 20/02/2026 | BA + Dev Lead | Audit trail & recovery |
| D-002 | JWT + localStorage | 20/02/2026 | Dev Lead | SPA standard |
| D-003 | Page size = 10 | 20/02/2026 | BA | UX + performance |
| D-004 | Export format = .xlsx | 20/02/2026 | BA | User familiarity |
| D-005 | Status mặc định = DRAFT | 20/02/2026 | BA | Business requirement |
| D-006 | File rename bằng UUID | 20/02/2026 | Dev Lead | Avoid conflicts |
| D-007 | Max file size = 20MB | 20/02/2026 | BA + Dev | Storage constraint |

---

## Deferred to V2.0

| Feature | Lý do defer |
|---|---|
| Tooltip giải thích DOI | Nice to have, users là researcher nên đã biết |
| Firefox/Mobile support | Tập trung Chrome cho V1.0 |
| Duplicate DOI warning (US-RES-019) | P1, không phải P0 |
| Auto-fetch metadata từ DOI (US-RES-020) | P2, cần CrossRef API integration |
| Import từ ORCID (US-RES-021) | P2, complex OAuth flow |
| Recovery/Restore deleted publications | V2.0 admin feature |

---

**Prepared by**: Business Analysis Team  
**Version**: 1.0  
**Date**: 20/02/2026  
**Review cycle**: Cập nhật mỗi khi có quyết định mới hoặc giả định được xác nhận/từ chối
