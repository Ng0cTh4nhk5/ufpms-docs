# Quy Trình Tìm Kiếm và Lọc - Biểu đồ Hoạt động

> 📊 **Biểu đồ**: Tìm kiếm & Lọc Ấn phẩm  
> 🎯 **Phạm vi**: Tìm kiếm công khai với nhiều bộ lọc  
> 👤 **Tác nhân**: Khách truy cập / Nhà nghiên cứu

---

## 📊 Biểu đồ Hoạt động

```mermaid
flowchart TD
    Start([Người dùng mở Trang Tìm kiếm]) --> LoadPage[Tải trang tìm kiếm]
    
    LoadPage --> FetchFilters[Lấy tùy chọn bộ lọc từ cơ sở dữ liệu]
    FetchFilters --> DisplaySearch[Hiển thị biểu mẫu tìm kiếm + kết quả trống]
    
    DisplaySearch --> UserAction{Hành động người dùng?}
    
    UserAction -->|Nhập từ khóa| EnterQuery[Gõ từ khóa tìm kiếm]
    EnterQuery --> CheckQuery{Độ dài truy vấn?}
    CheckQuery -->|< 3 ký tự| ShowHint[Hiển thị: "Tối thiểu 3 ký tự"]
    ShowHint --> EnterQuery
    CheckQuery -->|>= 3 ký tự| ApplyFilters
    
    UserAction -->|Chọn bộ lọc| SelectYear[Chọn khoảng năm]
    SelectYear --> SelectType[Chọn loại ấn phẩm]
    SelectType --> SelectFaculty[Chọn khoa (tùy chọn)]
    SelectFaculty --> ApplyFilters{Áp dụng tìm kiếm?}
    
    ApplyFilters -->|Nhấn Tìm kiếm| BuildQuery[Xây dựng truy vấn tìm kiếm]
    
    BuildQuery --> CheckAuth{Người dùng đã xác thực?}
    
    CheckAuth -->|Không: Công khai| AddPublicFilter[Thêm bộ lọc: trạng thái = PUBLISHED]
    AddPublicFilter --> ExecuteSearch
    
    CheckAuth -->|Có: Nhà nghiên cứu| AddResearcherFilter[Thêm bộ lọc: PUBLISHED HOẶC chủ sở hữu = userId]
    AddResearcherFilter --> ExecuteSearch
    
    ExecuteSearch[Thực hiện tìm kiếm toàn văn] --> GetResults[Lấy từ cơ sở dữ liệu]
    
    GetResults --> CheckResults{Tìm thấy kết quả?}
    
    CheckResults -->|Không có kết quả| ShowEmpty[Hiển thị: Không tìm thấy ấn phẩm + gợi ý]
    ShowEmpty --> UserAction
    
    CheckResults -->|Có kết quả| SortResults[Sắp xếp theo mức độ liên quan sau đó năm giảm dần]
    
    SortResults --> Paginate[Áp dụng phân trang 20 mỗi trang]
    
    Paginate --> DisplayResults[Hiển thị danh sách kết quả]
    
    DisplayResults --> UserNext{Hành động người dùng?}
    
    UserNext -->|Nhấn vào ấn phẩm| ViewDetail[Chuyển hướng đến trang chi tiết ấn phẩm]
    ViewDetail --> End1([Kết thúc])
    
    UserNext -->|Đổi trang| ChangePage[Đi đến trang N]
    ChangePage --> Paginate
    
    UserNext -->|Sửa đổi bộ lọc| UserAction
    
    UserNext -->|Xuất kết quả| ExportCSV[Xuất ra CSV tính năng P2]
    ExportCSV --> End2([Tải xuống tệp])
    
    style Start fill:#e3f2fd
    style End1 fill:#c8e6c9
    style End2 fill:#c8e6c9
    style DisplayResults fill:#fff9c4
    style ShowEmpty fill:#ffcdd2
```

---

## 📋 Tính Năng Tìm Kiếm

### 1. Tìm Kiếm Toàn Văn
**Các trường được tìm kiếm**:
- Tiêu đề (trọng số cao nhất)
- Tóm tắt
- Từ khóa
- Tên tác giả

**Truy vấn**:
```sql
MATCH(title, abstract, keywords) AGAINST ('query' IN NATURAL LANGUAGE MODE)
```

### 2. Bộ Lọc

| Bộ Lọc | Tùy Chọn | Mặc Định |
|--------|---------|---------|
| **Năm** | 1900-hiện tại, khoảng | Tất cả các năm |
| **Loại Ấn Phẩm** | Tạp chí, Hội nghị, Sách, v.v. | Tất cả các loại |
| **Khoa** | Danh sách từ cơ sở dữ liệu | Tất cả các khoa |
| **Có PDF** (P1) | Hộp kiểm Có/Không | Tất cả |
| **Tứ phân vị** (P2) | Q1, Q2, Q3, Q4 | Tất cả |

### 3. Sắp Xếp

**Mặc định**: Mức độ liên quan giảm dần, Năm giảm dần

**Tùy chọn** (P1):
- Mới nhất trước
- Cũ nhất trước
- Tiêu đề A-Z
- Số lượng trích dẫn (P2)

### 4. Phân Trang
- 20 kết quả mỗi trang
- Số trang: 1, 2, 3... (tối đa 10 hiển thị)
- Nút "Trước" / "Sau"

---

## 👁️ Quy Tắc Hiển Thị

### Khách Truy Cập (Chưa Xác Thực)
```sql
WHERE status = 'PUBLISHED'
```
**Có thể xem**: Chỉ các ấn phẩm đã xuất bản

### Nhà Nghiên Cứu (Đã Xác Thực)
```sql
WHERE status = 'PUBLISHED' 
   OR owner_id = {current_user_id}
```
**Có thể xem**: Đã xuất bản + ấn phẩm của chính mình (mọi trạng thái)

---

## 📊 Hiển Thị Kết Quả

Mỗi kết quả hiển thị:
- **Tiêu đề** (có thể nhấn vào)
- **Tác giả** (3 người đầu tiên, sau đó "et al.")
- **Năm**, **Loại** (Tạp chí/Hội nghị)
- **Tên Tạp chí/Hội nghị**
- **DOI** (nếu có)
- **Huy hiệu PDF** (nếu PDF đã được tải lên)

**Nổi bật**: Từ khóa tìm kiếm được tô sáng màu vàng

---

## 🚨 Các Tình Huống Biên

### Kết Quả Trống
**Thông báo**: "Không tìm thấy ấn phẩm nào phù hợp với tiêu chí của bạn"

**Gợi ý**:
- Thử ít bộ lọc hơn
- Kiểm tra chính tả
- Thử các từ khóa khác

### Truy Vấn Quá Ngắn
**Thông báo**: "Vui lòng nhập ít nhất 3 ký tự"

### Quá Nhiều Kết Quả
**Thông báo**: "Đang hiển thị 1000 kết quả hàng đầu. Vui lòng tinh chỉnh tìm kiếm của bạn."
(Giới hạn: tối đa 1000 kết quả = 50 trang)

---

## ⏱️ Hiệu Năng

**Mục tiêu**: < 500ms thời gian phản hồi

**Tối ưu hóa**:
- Chỉ mục toàn văn trên tiêu đề, tóm tắt, từ khóa
- Bộ nhớ đệm cho các tìm kiếm phổ biến (P1)
- Tối ưu hóa truy vấn cơ sở dữ liệu

---

**Liên quan**: UC-D3-01, seq_search_publications.md  
**Ngày tạo**: 11/02/2026
