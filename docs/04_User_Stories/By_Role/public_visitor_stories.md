# User Stories - Public Visitor

> 👤 **Role**: Public Visitor (Khách truy cập)  
> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Mục tiêu**: Tìm kiếm và xem thông tin công trình công bố, profile giảng viên

---

## Tổng Quan

**Total Stories**: 8  
**P0 (Must Have)**: 2  
**P1 (Should Have)**: 4  
**P2 (Nice to Have)**: 2

---

## Module 3: Search & Browse

### US-VIW-001: Tìm Kiếm Full-Text
**Priority**: 🟡 P1 - Should Have  
**Related FR**: FR-SEA-001

**User Story**:
```
As a public visitor (Là khách truy cập),
I want to search for publications using keywords (Tôi muốn tìm kiếm bài báo bằng từ khóa),
So that I can find research relevant to my interests (Để tôi có thể tìm thấy các nghiên cứu phù hợp với quan tâm của mình).
```

**Acceptance Criteria**:
```
GIVEN I am on the search page (no login required) (KHI tôi ở trang tìm kiếm - không cần đăng nhập)
WHEN I enter keywords and click search (VÀ tôi nhập từ khóa và nhấn tìm kiếm)
THEN I see results showing ONLY PUBLISHED publications (THÌ tôi thấy kết quả CHỈ hiện các bài báo ĐÃ CÔNG BỐ)
WHERE the search matches: Title, Abstract, Keywords, Author names (KHI tìm kiếm khớp với: Tiêu đề, Tóm tắt, Từ khóa, Tên tác giả)
AND matching keywords are highlighted (VÀ từ khóa khớp được làm nổi bật)
AND results are sorted by relevance (VÀ kết quả được sắp xếp theo độ tương quan)
```

---

### US-VIW-002: Lọc Kết Quả Nâng Cao
**Priority**: 🟡 P1 - Should Have  
**Related FR**: FR-SEA-002

**User Story**:
```
As a public visitor (Là khách truy cập),
I want to filter search results by various criteria (Tôi muốn lọc kết quả tìm kiếm theo nhiều tiêu chí),
So that I can narrow down to specific types of publications (Để tôi có thể thu hẹp phạm vi vào các loại bài báo cụ thể).
```

**Acceptance Criteria**:
```
GIVEN I have search results (KHI tôi có kết quả tìm kiếm)
WHEN I apply filters (VÀ tôi áp dụng bộ lọc)
THEN I can filter by: (THÌ tôi có thể lọc theo:)
- Year range (from year - to year) (Khoảng thời gian: từ năm - đến năm)
- Faculty/Department (Khoa/Phòng ban)
- Journal Type (Q1/Q2/Q3/Q4/Conference) (Loại tạp chí: Q1/Q2/Q3/Q4/Hội nghị)
- Publication Type (Journal/Conference) (Loại bài báo: Tạp chí/Hội nghị)
- Research Field (Lĩnh vực nghiên cứu)
AND results update dynamically (VÀ kết quả cập nhật động)
```

---

### US-VIW-003: Duyệt Theo Danh Mục
**Priority**: 🟡 P1 - Should Have  
**Related FR**: FR-SEA-003

**User Story**:
```
As a public visitor (Là khách truy cập),
I want to browse publications by category (Tôi muốn duyệt bài báo theo danh mục),
So that I can explore research without needing specific keywords (Để tôi có thể khám phá nghiên cứu mà không cần từ khóa cụ thể).
```

**Acceptance Criteria**:
```
GIVEN I click "Browse" (KHI tôi nhấn "Duyệt")
WHEN the page loads (VÀ trang tải xong)
THEN I see category options: (THÌ tôi thấy các tùy chọn danh mục:)
- By Faculty (Theo Khoa)
- By Year (Theo Năm)
- By Research Field (Theo Lĩnh vực nghiên cứu)
- By Journal Quartile (Q1/Q2/Q3/Q4) (Theo Phân hạng tạp chí)
AND clicking a category shows publications in that category (VÀ nhấn vào danh mục sẽ hiển thị các bài báo thuộc danh mục đó)
```

---

### US-VIW-004: Sắp Xếp Kết Quả
**Priority**: 🟡 P1 - Should Have  
**Related FR**: FR-SEA-007

**User Story**:
```
As a public visitor (Là khách truy cập),
I want to sort search results by different criteria (Tôi muốn sắp xếp kết quả tìm kiếm theo các tiêu chí khác nhau),
So that I can find the most relevant or recent publications first (Để tôi có thể tìm thấy bài báo phù hợp nhất hoặc mới nhất trước).
```

**Acceptance Criteria**:
```
GIVEN I have search results (KHI tôi có kết quả tìm kiếm)
WHEN I select a sort option (VÀ tôi chọn tùy chọn sắp xếp)
THEN results can be sorted by: (THÌ kết quả có thể được sắp xếp theo:)
- Newest first (default) (Mới nhất trước - mặc định)
- Oldest first (Cũ nhất trước)
- Most cited (Được trích dẫn nhiều nhất)
- Impact Factor (high to low) (Chỉ số ảnh hưởng - cao đến thấp)
```

---

### US-VIW-005: Phân Trang Kết Quả
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-SEA-005

**User Story**:
```
As a public visitor (Là khách truy cập),
I want search results to be paginated (Tôi muốn kết quả tìm kiếm được phân trang),
So that the page loads quickly and I can navigate through results (Để trang tải nhanh và tôi có thể duyệt qua các kết quả).
```

**Acceptance Criteria**:
```
GIVEN I have search results (KHI tôi có kết quả tìm kiếm)
WHEN viewing the results (VÀ xem kết quả)
THEN I see: (THÌ tôi thấy:)
- Default: 20 results per page (Mặc định: 20 kết quả mỗi trang)
- Pagination controls (1, 2, 3... Next) (Điều khiển phân trang: 1, 2, 3... Tiếp)
- Options to show: 10, 20, 50, or 100 results per page (Tùy chọn hiển thị: 10, 20, 50, hoặc 100 kết quả mỗi trang)
- Optional: Infinite scroll (Tùy chọn: Cuộn vô hạn)
```

---

### US-VIW-006: Xem Chi Tiết Công Trình
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-SEA-006

**User Story**:
```
As a public visitor (Là khách truy cập),
I want to view detailed information about a publication (Tôi muốn xem thông tin chi tiết về bài báo),
So that I can read the full metadata and access the paper (Để tôi có thể đọc đầy đủ thông tin và truy cập bài báo).
```

**Acceptance Criteria**:
```
GIVEN I click on a publication from search results (KHI tôi nhấn vào một bài báo từ kết quả tìm kiếm)
WHEN the detail page loads (VÀ trang chi tiết tải xong)
THEN I see: (THÌ tôi thấy:)
- Full metadata (title, authors, journal, year, abstract, etc.) (Thông tin đầy đủ: tiêu đề, tác giả, tạp chí, năm, tóm tắt, v.v.)
- DOI link (clickable to external source) (Link DOI - có thể nhấn để đến nguồn ngoài)
- Download PDF button (if allowed) (Nút tải PDF - nếu được phép)
- Links to author profiles (Link đến hồ sơ tác giả)
```

---

### US-VIW-007: Export Kết Quả Tìm Kiếm
**Priority**: 🟢 P2 - Nice to Have  
**Related FR**: FR-SEA-004

**User Story**:
```
As a public visitor (Là khách truy cập),
I want to export search results in various formats (Tôi muốn xuất kết quả tìm kiếm ra nhiều định dạng),
So that I can use them in reference managers or spreadsheets (Để tôi có thể dùng trong các phần mềm quản lý trích dẫn hoặc bảng tính).
```

**Acceptance Criteria**:
```
GIVEN I have search results (KHI tôi có kết quả tìm kiếm)
WHEN I click "Export" (VÀ tôi nhấn "Xuất")
THEN I can choose format: (THÌ tôi có thể chọn định dạng:)
- BibTeX (for LaTeX) (BibTeX - cho LaTeX)
- RIS (for EndNote, Mendeley, Zotero) (RIS - cho EndNote, Mendeley, Zotero)
- CSV (for Excel) (CSV - cho Excel)
- JSON (for developers) (JSON - cho lập trình viên)
AND the file is downloaded with the selected results (VÀ file được tải xuống với các kết quả đã chọn)
```

---

## Module 4: Researcher Profile (View Only)

### US-VIW-008: Xem Profile Giảng Viên
**Priority**: 🟢 P2 - Nice to Have  
**Related FR**: FR-PRO-001, FR-PRO-006

**User Story**:
```
As a public visitor (Là khách truy cập),
I want to view a researcher's public profile (Tôi muốn xem hồ sơ công khai của giảng viên),
So that I can learn about their research and publications (Để tôi có thể tìm hiểu về nghiên cứu và bài báo của họ).
```

**Acceptance Criteria**:
```
GIVEN I access a researcher's profile URL (/profile/[username]) (KHI tôi truy cập URL hồ sơ giảng viên)
WHEN the page loads (VÀ trang tải xong)
THEN I see: (THÌ tôi thấy:)
- Profile photo, name, title, faculty (Ảnh, tên, chức danh, khoa)
- Contact information (email, ORCID) (Thông tin liên hệ: email, ORCID)
- Bio and research interests (Tiểu sử và hướng nghiên cứu)
- List of PUBLISHED publications only (Danh sách bài báo ĐÃ CÔNG BỐ)
- Publications per year chart (Biểu đồ bài báo theo năm)
- Research field word cloud (Word cloud lĩnh vực nghiên cứu)
AND I can click on publications to view details (VÀ tôi có thể nhấn vào bài báo để xem chi tiết)
AND the page is SEO-optimized with proper meta tags (VÀ trang được tối ưu SEO với các thẻ meta phù hợp)
```

---

## Traceability Matrix

| Story ID | Title | Priority | FR ID | Module |
|----------|-------|----------|-------|--------|
| US-VIW-001 | Tìm Kiếm Full-Text | P1 | FR-SEA-001 | 3 |
| US-VIW-002 | Lọc Kết Quả Nâng Cao | P1 | FR-SEA-002 | 3 |
| US-VIW-003 | Duyệt Theo Danh Mục | P1 | FR-SEA-003 | 3 |
| US-VIW-004 | Sắp Xếp Kết Quả | P1 | FR-SEA-007 | 3 |
| US-VIW-005 | Phân Trang Kết Quả | P0 | FR-SEA-005 | 3 |
| US-VIW-006 | Xem Chi Tiết Công Trình | P0 | FR-SEA-006 | 3 |
| US-VIW-007 | Export Kết Quả Tìm Kiếm | P2 | FR-SEA-004 | 3 |
| US-VIW-008 | Xem Profile Giảng Viên | P2 | FR-PRO-001, FR-PRO-006 | 4 |

---

**Tài liệu liên quan**:
- [Requirements - Search & Browse](../../03_Requirements/Functional/module_search.md)
- [Requirements - Researcher Profile](../../03_Requirements/Functional/module_profile.md)
