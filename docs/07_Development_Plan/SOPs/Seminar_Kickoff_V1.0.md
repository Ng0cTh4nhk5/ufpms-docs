# 🚀 UFPMS Version 1.0 - Kickoff Seminar

> **Mục tiêu Seminar**: Khởi động giai đoạn phát triển Phiên bản 1.0 (V1.0), thống nhất quy trình làm việc (SOPs), phạm vi công việc và trách nhiệm của từng thành viên trong team.
> **Thời lượng dự kiến**: 45 - 60 phút.
> **Tài liệu tham khảo chính**: [Bộ SOPs V1.0](./README.md) và [Nội quy GitHub Repository](../github_repository_rules.md).

---

## Phần 1: Tổng Quan Mục Tiêu & Phạm Vi V1.0 (10 phút)

**Người trình bày: Product Manager (PM)**

### 1.1 Khẳng định Mục tiêu V1.0
- V1.0 là phiên bản MVP (Minimum Viable Product) tập trung vào core flow: **Quản lý ấn phẩm khoa học (Publication Management)**.
- Phục vụ trực tiếp cho đối tượng Researcher (Giảng viên/Nghiên cứu viên).

### 1.2 Phạm Vi Tính Năng (Scope)
Chỉ tập trung vào **9 User Stories** cốt lõi:
1. Tạo bài báo mới (Draft)
2. Upload file PDF minh chứng
3. Sửa bài báo nháp
4. Xóa bài báo nháp
5. Xem danh sách bài báo của mình
6. Thêm đồng tác giả
7. Xem chi tiết bài báo
8. Download file PDF minh chứng
9. Xem dashboard giờ làm quy đổi

**Kết quả đầu ra UI**: 6 Screens chính (Login, Dashboard, List, Create form, Edit form, Detail view).

---

## Phần 2: Quy Trình Phát Triển 3 Phases (15 phút)

**Người trình bày: Tech Lead / PM**

Quy trình phát triển V1.0 được chia thành 3 giai đoạn (Phases) rõ ràng, mang tính kết nối giữa các role:

### 📐 Phase 1: DESIGN (Thiết kế & Lên Kế Hoạch)
- **UI/UX**: Hoàn thiện Design System & chuẩn bị thiết kế 6 screens trên Figma.
- **BA**: Chốt lại Acceptance Criteria cho 9 US, hỗ trợ QA viết test scenarios.
- **Tech Lead & Dev (FE/BE)**: Chốt kiến trúc hệ thống, thống nhất APIs spec, Database schema, Setup Repo & CI/CD.
- **QA**: Lập Test Plan toàn diện, chuẩn bị viết test cases chuyên sâu.

### 💻 Phase 2: DEVELOPMENT (Phát Triển)
- **Frontend & Backend**: Bắt đầu code theo UI design và specs API. Triển khai viết Unit Tests đồng thời.
- **UI/UX**: Hỗ trợ Dev thẩm định (QA) giao diện, đảm bảo bám sát thiết kế.
- **QA**: Thực hiện Test API (qua Postman), test UI liên tục khi merge tính năng lên nhánh `develop`.
- **PM/Tech Lead**: Điều hành Daily standup, Tech Lead review code nghiêm ngặt.

### ✅ Phase 3: VERIFICATION (Kiểm Thử & Đóng Gói)
- **QA**: Regression test (kiểm thử hồi quy) toàn bộ hệ thống, báo cáo bugs kịp thời.
- **Dev**: Cập nhật fix bugs, hoàn thiện trải nghiệm UI/UX cuối cùng.
- **BA & PM**: Tiến hành UAT (User Acceptance Testing), ký nghiệm thu nội bộ, chuẩn bị kịch bản Demo.
- **Tech Lead**: Rà soát tiêu chuẩn an toàn (Pre-release checklist), Deploy lên Staging/Production chuẩn bị Release.

---

## Phần 3: Vai Trò & SOPs của Từng Thành Viên (10 phút)

**Người trình bày: Đại diện từng Role (1-2 phút/người) hoặc PM tổng hợp**

Mọi thành viên **BẮT BUỘC** phải đọc và tuân thủ SOP cá nhân của mình từ thư mục SOPs:
- 👑 **PM** ([SOP_PM_V1.0.md](./SOP_PM_V1.0.md)): Quản lý Scope, ngăn chặn rủi ro "Scope Creep", theo dõi timeline.
- 📋 **BA** ([SOP_BA_V1.0.md](./SOP_BA_V1.0.md)): Cầu nối requirement, giải đáp mọi thắc mắc logic nghiệp vụ cho team.
- 🎨 **UI/UX** ([SOP_UIUX_V1.0.md](./SOP_UIUX_V1.0.md)): Cung cấp và bàn giao Figma, hỗ trợ review design trên frontend hoàn thiện.
- ⚙️ **Backend** ([SOP_Backend_V1.0.md](./SOP_Backend_V1.0.md)): Phát triển APIs, Cơ sở dữ liệu, xử lý file upload, Authentication.
- 🖥️ **Frontend** ([SOP_Frontend_V1.0.md](./SOP_Frontend_V1.0.md)): Xây dựng React UI, tích hợp APIs, đảm bảo Responsive tốt.
- 🐞 **QA/Tester** ([SOP_QA_V1.0.md](./SOP_QA_V1.0.md)): Gatekeeper chất lượng cuối cùng, quản lý test plan và lifecycle của bug.
- 🏗️ **Tech Lead** ([SOP_TechLead_V1.0.md](./SOP_TechLead_V1.0.md)): Quyết định Architecture, quản trị CI/CD và định hướng kỹ thuật chung.

---

## Phần 4: Quy Tắc Kỹ Thuật & Môi Trường Làm Việc (10 phút)

**Người trình bày: Tech Lead**

### 4.1 Quy tắc GitHub & Quản Lý Mã Nguồn
- **Mô hình Nhánh (Branch Strategy)**: Sử dụng GitFlow Lite (gồm `main`, `develop`, `feature/*`, `bugfix/*`).
- **Branch Protection Rules**: Các nhánh `main` và `develop` đã được khoá. Nghiêm cấm push code trực tiếp.
- **Quy trình Merge Code (PR)**: Mọi thay đổi phải tạo Pull Request (PR) -> Phải qua CI/CD Pass (Build & Test thành công) -> Yêu cầu ít nhất 1 Approve từ người review (Tech Lead/Dev).
- **Commit Message Convention**: Tuân thủ chuẩn Conventional Commits (`feat:`, `fix:`, `docs:`, `refactor:`, `test:`, ...).

### 4.2 Văn Hóa Giao Tiếp & Xử Lý Blocker
- Mọi khó khăn/blockers cần được escalate ngay lập tức trong Daily Standup.
- **Nguyên tắc "Đúng người, Đúng việc"**:
  - Không rõ luồng logic, requirement? ➡️ Hỏi **BA**.
  - Không rõ màu sắc, component giao diện? ➡️ Check **Figma** / Hỏi **UI/UX**.
  - Không rõ Technical flow, architecture? ➡️ Hỏi **Tech Lead** hoặc **Backend/Frontend Team**. 
- 🚫 **Tuyệt đối không tự ý giả định (assume)** yêu cầu. Nếu không chắc chắn, hãy chủ động **HỎI**.

---

## Phần 5: Definition of DONE & Next Steps (5 phút)

**Người trình bày: PM**

### 5.1 Khi nào chúng ta chính thức hoàn thành V1.0?
- [ ] Code hoàn thành đáp ứng 9 User Stories và 6 Screens định trước.
- [ ] Đạt 100% Acceptance Criteria của các tính năng.
- [ ] Qua các bước Manual Testing & QA Sign-off (Không có bug Critical/High tồn đọng).
- [ ] Unit Test đạt mức chỉ tiêu: Backend >= 80%, Frontend >= 70%.
- [ ] Dự án được merged vào branch `main` an toàn và triển khai thành công, sẵn sàng Demo.

### 5.2 Next Steps ngay sau buổi Kickoff
1. **Hôm nay**: Các cá nhân tự rà soát, đọc kỹ tệp [SOP của vai trò mình](./README.md) tối thiểu 1 lần.
2. **Kỹ thuật**: Các Dev clone source code, setup môi trường local.
3. **Triển khai Phase 1 (DESIGN)**: Bắt tay ngay vào việc chốt kiến trúc, thiết kế DB và chuẩn bị specs API/UI trong thời gian quy định.
4. Hẹn gặp lại toàn team ở buổi Daily Standup ngày mai!

---
*💡 Let's build a high-quality V1.0 together! Chúc team chặng đường phát triển V1.0 thuận lợi và thành công!*
