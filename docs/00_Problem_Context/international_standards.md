# Chuẩn Mực và Thực Tiễn Quốc Tế về Quản Lý Nghiên Cứu Khoa Học

> **Mục đích**: Cung cấp bối cảnh quốc tế để hiểu rõ hơn về các tiêu chuẩn và phương pháp hay nhất trong quản lý công trình NCKH, làm nền tảng tham khảo cho thiết kế hệ thống.

---

## 1. Tiêu Chuẩn Quản Lý Thông Tin Nghiên Cứu

### 1.1. CERIF (Common European Research Information Format)

**Nguồn gốc**: Châu Âu  
**Mục đích**: Tiêu chuẩn vàng cho việc trao đổi dữ liệu nghiên cứu giữa các tổ chức

**Cấu trúc thực thể CERIF 1.3:**

| Loại Thực thể | Mô tả | Ví dụ Cụ thể |
|---------------|-------|--------------|
| **Thực thể Cơ sở** | Tác nhân và dự án cốt lõi | Person (Nhà nghiên cứu), OrganisationUnit (Đơn vị), Project (Dự án) |
| **Thực thể Kết quả** | Đầu ra hữu hình/vô hình | ResultPublication (Bài báo), ResultPatent (Bằng sáng chế), ResultProduct (Sản phẩm) |
| **Thực thể Hạ tầng** | Nguồn lực vật chất | Facility (Cơ sở vật chất), Equipment (Thiết bị), Service (Dịch vụ) |
| **Thực thể Liên kết** | Quan hệ ngữ nghĩa có thời gian | Quan hệ Người-Dự án (Vai trò: Chủ nhiệm/Thành viên) |

**Ứng dụng vào module bài báo:**
- Metadata của bài báo nên tuân thủ cấu trúc CERIF ResultPublication
- Liên kết tác giả-bài báo nên có vai trò (Tác giả chính, Đồng tác giả, Tác giả liên hệ)
- Sử dụng định danh vĩnh viễn (DOI, ORCID)

---

### 1.2. VIVO (Mô hình Bắc Mỹ)

**Nguồn gốc**: Hoa Kỳ  
**Công nghệ**: Web ngữ nghĩa (Semantic Web), Linked Open Data

**Đặc điểm:**
- Sử dụng URIs để định danh vĩnh viễn
- Tuân thủ nguyên tắc FAIR (Findable, Accessible, Interoperable, Reusable)
- Tạo mạng lưới dữ liệu mở liên kết

**Bài học cho module bài báo:**
- Mỗi bài báo, tác giả nên có ID duy nhất (UUID)
- API nên thiết kế để dễ dàng kết nối với hệ thống khác
- Profile giảng viên có thể export dạng RDF để tích hợp

---

### 1.3. Hệ Thống CRIS Phổ Biến

**Pure (Elsevier):**
- Quản lý toàn diện: Nghiên cứu, Giảng dạy, Tác động
- Tích hợp Scopus, Web of Science
- Dashboard phân tích mạnh

**Symplectic Elements:**
- Tự động thu thập công bố từ nhiều nguồn
- Workflow phê duyệt linh hoạt

**DSpace:**
- Mã nguồn mở
- Tập trung vào lưu trữ (Institutional Repository)

**Bài học:**
- Module bài báo của ta cần có API để tích hợp với các hệ thống lớn hơn sau này
- Workflow phê duyệt quan trọng để đảm bảo chất lượng dữ liệu

---

## 2. Tiêu Chuẩn Phân Loại và Đánh Giá

### 2.1. OECD Frascati Manual

**Phân loại R&D:**
- **Nghiên cứu cơ bản**: Tăng hiểu biết mà không nhắm ứng dụng cụ thể
- **Nghiên cứu ứng dụng**: Hướng đến mục tiêu thực tiễn
- **Phát triển thực nghiệm**: Tạo ra sản phẩm/quy trình mới

**Áp dụng:**
- Có thể tag bài báo theo loại R&D để phân tích sau này
- Giúp phân biệt nghiên cứu lý thuyết vs ứng dụng

---

### 2.2. Oslo Manual (Đổi mới sáng tạo)

**Định nghĩa quan trọng:**
> Đổi mới phải là sản phẩm đã được **giới thiệu ra thị trường** hoặc áp dụng thực tế

**4 loại đổi mới:**
1. Sản phẩm (Product innovation)
2. Quy trình (Process innovation)
3. Marketing (Marketing innovation)
4. Tổ chức (Organizational innovation)

**Liên quan đến module:**
- Bài báo về đổi mới nên được gắn tag để dễ tìm kiếm
- Theo dõi xem bài báo nào dẫn đến ứng dụng thực tế

---

### 2.3. COAR Resource Types

**Phân loại tài nguyên số:**
- Journal articles (Bài báo tạp chí) ← Module ta tập trung vào đây
- Conference papers (Bài hội thảo)
- Datasets (Dữ liệu nghiên cứu)
- Software (Phần mềm)
- Workflows (Quy trình)

**Bài học:**
- Thiết kế database linh hoạt để sau này có thể thêm các loại khác (Dataset, Software...)
- Metadata structure nên tương thích để dễ mở rộng

---

## 3. Định Danh và Xếp Hạng

### 3.1. CRediT (Contributor Roles Taxonomy)

**14 vai trò đóng góp:**
1. Conceptualization (Hình thành ý tưởng)
2. Data curation (Quản lý dữ liệu)
3. Formal analysis (Phân tích)
4. Funding acquisition (Tìm kiếm tài trợ)
5. Investigation (Điều tra, thực nghiệm)
6. Methodology (Phương pháp luận)
7. Project administration (Quản lý dự án)
8. Resources (Nguồn lực)
9. Software (Phần mềm)
10. Supervision (Giám sát)
11. Validation (Kiểm chứng)
12. Visualization (Trực quan hóa)
13. Writing - original draft (Viết bản thảo)
14. Writing - review & editing (Biên tập)

**Ứng dụng:**
- Thêm trường "Contributor Role" khi thêm đồng tác giả
- Ghi nhận đóng góp công bằng hơn
- Hữu ích cho đánh giá KPI chi tiết

---

### 3.2. Persistent Identifiers (Định danh vĩnh viễn)

**DOI (Digital Object Identifier):**
- Cho bài báo, dataset, protocol
- Dạng: `10.1000/xyz123`
- Quản lý bởi CrossRef, DataCite

**ORCID (Open Researcher and Contributor ID):**
- Cho nhà nghiên cứu
- Dạng: `0000-0002-1825-0097`
- Giải quyết vấn đề trùng tên

**ISSN (International Standard Serial Number):**
- Cho tạp chí
- Dạng: `0028-0836` (Nature)

**Khuyến nghị cho module:**
- Lưu DOI, ORCID, ISSN khi có
- Validation format khi nhập
- Tích hợp API để tự động lấy metadata từ DOI (CrossRef API)

---

## 4. Mô Hình Chuyển Giao Công Nghệ

### 4.1. Bayh-Dole Act (Mỹ, 1980)

**Nội dung chính:**
- Trao quyền sở hữu trí tuệ từ nghiên cứu công cho đại học/viện
- Đại học có thể cấp phép độc quyền cho doanh nghiệp
- Khuyến khích thành lập spin-off companies

**Kết quả:**
- Tăng đột biến số lượng patent từ đại học
- Doanh thu từ licensing: hàng tỷ USD/năm
- Thung lũng Silicon xuất hiện các startup từ Stanford, MIT

**Bài học cho Việt Nam:**
- Cần cơ chế tương tự để khuyến khích thương mại hóa
- TTO (Technology Transfer Office) cần được tăng cường

---

## 5. Phương Pháp Quản Lý Dự Án Nghiên Cứu

### 5.1. Traditional Waterfall vs Agile

**Waterfall (Truyền thống):**
```
Lập kế hoạch → Thực hiện → Đánh giá → Nghiệm thu
(Tuần tự, khó thay đổi)
```

**Agile/Scrum (Linh hoạt):**
```
Sprint 1 (2-4 tuần) → Review → Sprint 2 → Review → ...
(Lặp lại, dễ điều chỉnh)
```

**Case Study: Đại học Leiden (Hà Lan):**
- Áp dụng Scrum với Sprint 4 tuần
- Daily stand-up meeting 15 phút
- Scrum board để theo dõi tiến độ

**Kết quả:**
- ✅ Tăng tính cộng tác
- ✅ Phát hiện vấn đề sớm
- ✅ Minh bạch đóng góp của từng thành viên

**Ứng dụng vào module:**
- Phát triển phần mềm nên dùng Agile
- Chia thành Sprint, mỗi Sprint có demo
- User feedback sớm để điều chỉnh

---

### 5.2. Quản Lý Tài Chính

**Lump Sum (Khoán trọn gói) - Horizon Europe:**
- Giải ngân dựa trên hoàn thành Work Package
- Không kiểm tra hóa đơn chi tiết
- Giảm gánh nặng hành chính

**Indirect Costs (Chi phí gián tiếp) - NSF (Mỹ):**
- Cho phép 40-60% chi phí gián tiếp
- Bù đắp chi phí vận hành tổ chức

**So sánh với Việt Nam:**
- VN: Vẫn nặng về kiểm soát chứng từ
- Khoán chi chưa phổ biến do lo rủi ro
- Cần chuyển dần sang quản lý theo đầu ra

---

## 6. Xu Hướng Mới

### 6.1. Open Science

**Nguyên tắc:**
- Open Access (Công bố mở)
- Open Data (Dữ liệu mở)
- Open Peer Review (Phản biện công khai)

**Áp dụng:**
- Module có thể có chức năng đánh dấu bài báo "Open Access"
- Khuyến khích upload preprint

---

### 6.2. FAIR Data Principles

**F**indable - Dễ tìm:
- Có metadata đầy đủ
- Đăng ký trong registry

**A**ccessible - Dễ truy cập:
- Protocol chuẩn (HTTP)
- Authentication rõ ràng

**I**nteroperable - Tương tác được:
- Sử dụng chuẩn chung (JSON, XML)
- Vocabulary chuẩn

**R**eusable - Tái sử dụng được:
- License rõ ràng
- Provenance (nguồn gốc) đầy đủ

**Khuyến nghị:**
- API của module nên tuân thủ FAIR
- Metadata export dạng standard format

---

## 7. So Sánh Việt Nam vs Quốc Tế

| Khía cạnh | Quốc tế (Mỹ/EU) | Việt Nam |
|-----------|------------------|----------|
| **Quản lý dữ liệu** | CERIF, VIVO (ngữ nghĩa) | STM (quy trình-based) |
| **Tài chính** | Lump sum, Indirect costs | Khoán từng phần, Hóa đơn chi tiết |
| **Chuyển giao** | Bayh-Dole, TTO mạnh | TTO yếu, cơ chế tài sản công phức tạp |
| **Đánh giá** | Tác động kinh tế-xã hội | Đếm số lượng sản phẩm |
| **Công khai** | Open Science, FAIR | Chưa phổ biến |

---

## 8. Khuyến Nghị Cho Module Bài Báo

Dựa trên phân tích trên, module bài báo khoa học nên:

### 8.1. Ngắn Hạn (MVP)

✅ **Metadata chuẩn:**
- Tuân thủ structure tương tự CERIF ResultPublication
- Lưu DOI, ORCID, ISSN

✅ **API-first:**
- RESTful API chuẩn OpenAPI
- Dễ tích hợp với hệ thống khác

✅ **Persistent ID:**
- UUID cho mỗi bài báo
- Slug URL thân thiện (SEO)

---

### 8.2. Trung Hạn (Phase 2)

🔸 **Tích hợp quốc tế:**
- CrossRef API - Tự động lấy metadata từ DOI
- ORCID API - Import publication list

🔸 **Contributor Roles:**
- Thêm field ghi nhận vai trò theo CRediT

🔸 **Export chuẩn:**
- BibTeX, RIS, EndNote XML
- JSON-LD (Linked Data)

---

### 8.3. Dài Hạn (Phase 3)

🔮 **Open Access tracking:**
- Đánh dấu bài báo OA
- Link đến preprint server (arXiv...)

🔮 **Research Impact:**
- Tích hợp Altmetric (social media mentions)
- Track citations qua Google Scholar/Scopus API

🔮 **FAIR compliance:**
- Metadata có thể harvest bởi OAI-PMH
- Machine-readable format

---

## 9. Tài Liệu Tham Khảo

**Chuẩn quốc tế:**
- CERIF: https://www.eurocris.org/cerif
- VIVO: https://duraspace.org/vivo/
- CRediT: https://credit.niso.org/
- FAIR: https://www.go-fair.org/

**Research Information Systems:**
- Pure: https://www.elsevier.com/solutions/pure
- Symplectic Elements: https://www.symplectic.co.uk/
- DSpace: https://dspace.org/

**Phân loại và đánh giá:**
- Frascati Manual: https://www.oecd.org/sti/frascati-manual.htm
- Oslo Manual: https://www.oecd.org/innovation/oslo-manual.htm

---

*Tài liệu này cung cấp bối cảnh quốc tế để thiết kế module bài báo theo chuẩn mực hiện đại, đảm bảo tính mở rộng và tương thích trong tương lai.*
