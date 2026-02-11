# Phân hệ 5: Báo cáo & Phân tích - Yêu Cầu Chức Năng

> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Phân hệ**: Báo cáo và Thống kê  
> 👥 **Người dùng**: Người duyệt cấp Trường, Người duyệt cấp Khoa, Quản trị viên cấp cao

---

## 1. Yêu Cầu Chức Năng

### FR-REP-001: Bảng điều khiển Phân tích (Dashboard Analytics)
**Độ ưu tiên**: 🟡 P1 - Nên Có

**Các chỉ số (Metrics)**:
- Tổng số bài báo (từ trước đến nay)
- Số bài báo năm nay
- Theo nhóm tứ phân vị (Q1/Q2/Q3/Q4)
- Theo Khoa
- Các nhà nghiên cứu hàng đầu

**Trực quan hóa**:
- Biểu đồ đường: Xu hướng theo năm
- Biểu đồ tròn: Phân bố theo nhóm tứ phân vị
- Biểu đồ cột: Theo Khoa

---

### FR-REP-002: Báo cáo theo Khoa
**Độ ưu tiên**: 🟡 P1 - Nên Có

**Tiêu chí chấp nhận**:
```
GIVEN chọn Khoa và Khoảng thời gian (năm)
WHEN tạo báo cáo
THEN xuất ra:
  - Danh sách bài báo
  - Nhóm theo nhà nghiên cứu
  - Thống kê tóm tắt
  - Định dạng Excel/PDF
```

---

### FR-REP-003: Báo cáo theo Nhóm tứ phân vị
**Độ ưu tiên**: 🟡 P1 - Nên Có

**Phân tích chi tiết**:
- Bài báo Q1
- Bài báo Q2
- Bài báo Q3/Q4
- Bài báo Hội nghị

---

### FR-REP-004: Phân tích Xu hướng
**Độ ưu tiên**: 🟢 P2 - Có Thể Có

**Hiển thị**:
- Tăng trưởng theo từng năm (Year-over-year)
- Các Khoa tăng trưởng hàng đầu
- Các lĩnh vực nghiên cứu mới nổi (từ từ khóa)

---

### FR-REP-005: Xuất Báo cáo
**Độ ưu tiên**: 🔴 P0 - Phải Có

**Định dạng**:
- Excel (.xlsx)
- PDF
- CSV

**Tốc độ**: < 5 phút (so với 2-3 ngày hiện tại)

---

### FR-REP-006: Báo cáo Định kỳ
**Độ ưu tiên**: 🟢 P2 - Có Thể Có

**Tự động tạo báo cáo hàng tháng/quý**:
- Gửi email cho lãnh đạo trường
- Lưu vào lưu trữ

---

### FR-REP-007: Nhà nghiên cứu Tiêu biểu
**Độ ưu tiên**: 🟡 P1 - Nên Có

**Xếp hạng theo**:
- Tổng số bài báo
- Số bài báo Q1
- Năng suất nhất trong năm nay

---

## 2. Quyền hạn

| Loại Báo cáo | Người duyệt Khoa | Người duyệt Trường | Admin |
|-------------|------------------|---------------------|------------|
| Báo cáo Khoa (của mình) | ✅ | ✅ | ✅ |
| Báo cáo Khoa (tất cả) | ❌ | ✅ | ✅ |
| Toàn trường | ❌ | ✅ | ✅ |
| Phân tích xu hướng | ❌ | ✅ | ✅ |

---

**Tài liệu liên quan**:
- [Nhu cầu Người dùng - Người duyệt cấp Trường](../../02_System_Clarification/User_Analysis/user_needs.md#3-university-reviewer)
