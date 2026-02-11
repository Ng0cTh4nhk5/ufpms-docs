# Phân hệ 3: Tìm kiếm & Tra cứu - Yêu Cầu Chức Năng

> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Phân hệ**: Tìm kiếm và Tra cứu Bài báo  
> 👥 **Người dùng**: Tất cả (Truy cập Công khai)

---

## 1. Yêu Cầu Chức Năng

### FR-SEA-001: Tìm kiếm Toàn văn (Full-Text Search)
**Độ ưu tiên**: 🟡 P1 - Nên Có

**Tiêu chí chấp nhận**:
```
GIVEN người dùng truy cập trang tìm kiếm
WHEN nhập từ khóa và tìm kiếm
THEN hiển thị kết quả chỉ công trình ĐÃ XUẤT BẢN:
  - Tìm trong: Tiêu đề, Tóm tắt, Từ khóa, Tên tác giả
  - Làm nổi bật từ khóa trong kết quả
  - Sắp xếp theo độ liên quan
```

---

### FR-SEA-002: Bộ lọc Nâng cao
**Độ ưu tiên**: 🟡 P1 - Nên Có

**Bộ lọc**:
- Năm (khoảng: từ năm - đến năm)  
- Khoa/Bộ môn  
- Loại Tạp chí (Q1/Q2/Q3/Q4 hoặc Hội nghị)  
- Loại Bài báo (Tạp chí/Hội nghị)  
- Lĩnh vực Nghiên cứu

---

### FR-SEA-003: Duyệt theo Danh mục
**Độ ưu tiên**: 🟡 P1 - Nên Có

**Tiêu chí chấp nhận**:
```
WHEN chọn "Duyệt" (Browse)
THEN hiển thị các danh mục:
  - Theo Khoa
  - Theo Năm
  - Theo Lĩnh vực Nghiên cứu
  - Theo Nhóm tứ phân vị Tạp chí
```

---

### FR-SEA-004: Xuất Kết quả Tìm kiếm
**Độ ưu tiên**: 🟢 P2 - Có Thể Có

**Định dạng xuất**:
- BibTeX
- RIS (cho các trình quản lý trích dẫn)
- CSV  
- JSON

---

### FR-SEA-005: Phân trang
**Độ ưu tiên**: 🔴 P0 - Phải Có

**Tiêu chí chấp nhận**:
- Mặc định: 20 kết quả/trang
- Tùy chọn: 10, 20, 50, 100
- Cuộn vô tận (tùy chọn)

---

### FR-SEA-006: Xem Chi tiết Bài báo (Công khai)
**Độ ưu tiên**: 🔴 P0 - Phải Có

**Tiêu chí chấp nhận**:
```
WHEN nhấn vào bài báo
THEN hiển thị:
  - Metadata đầy đủ
  - Liên kết DOI
  - Tải xuống PDF (nếu cho phép)
  - Hồ sơ tác giả (liên kết đến hồ sơ)
```

---

### FR-SEA-007: Tùy chọn Sắp xếp
**Độ ưu tiên**: 🟡 P1 - Nên Có

**Sắp xếp theo**:
- Mới nhất trước (mặc định)
- Cũ nhất trước  
- Được trích dẫn nhiều nhất  
- Chỉ số ảnh hưởng (cao xuống thấp)

---

## 2. Yêu Cầu Phi Chức Năng

**Hiệu năng**:
- Thời gian phản hồi tìm kiếm < 1 giây (10,000 bài báo)
- Hỗ trợ tìm kiếm mờ (fuzzy search)
- Đánh chỉ mục với Elasticsearch (tùy chọn)

**SEO**:
- Thẻ Meta cho từng trang bài báo
- Sitemap.xml
- Robots.txt

---

**Tài liệu liên quan**:
- [Phân hệ 4: Hồ sơ Nhà nghiên cứu](./module_profile.md)
