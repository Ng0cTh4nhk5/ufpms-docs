# Toàn Cảnh Bài Toán: Quản Lý Công Trình Nghiên Cứu Khoa Học tại Việt Nam

> **Mục đích folder này**: Mô tả bối cảnh TỔNG QUÁT của bài toán quản lý công trình NCKH, để hiểu rõ vị trí và giá trị của đồ án trong bức tranh lớn hơn.

---

## 📌 Quan Hệ Giữa Toàn Cảnh và Đồ Án

```
┌─────────────────────────────────────────────────────────────┐
│  TOÀN CẢNH: Hệ thống quản lý TOÀN BỘ công trình NCKH       │
│  - 7 nhóm công trình (28 loại)                              │
│  - Áp dụng cho: Bộ KH&CN, Đại học, Viện nghiên cứu        │
│  - Tuân thủ đầy đủ 8 văn bản pháp luật                     │
│                                                              │
│  ┌────────────────────────────────────────────────────┐   │
│  │  PHẠM VI ĐỒ ÁN (Module con):                       │   │
│  │  Quản lý BÀI BÁO KHOA HỌC của Giảng viên          │   │
│  │  - Chỉ 1 loại công trình: Bài báo (Publications)   │   │
│  │  - Chỉ 1 đối tượng: Giảng viên                     │   │
│  │  - Chỉ 1 cơ quan: Trường Đại học                   │   │
│  └────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
```

---

## 1. Toàn Cảnh Bài Toán

### 1.1. Định Nghĩa

**Công trình nghiên cứu khoa học** là sản phẩm hữu hình/vô hình được tạo ra từ hoạt động nghiên cứu, phát triển công nghệ, và đổi mới sáng tạo.

Theo pháp luật Việt Nam (Luật KH, CN & ĐMST 2025), các công trình này được phân thành **7 nhóm chính** với **28 loại cụ thể**.

---

### 1.2. Bảy Nhóm Công Trình NCKH

#### **Nhóm 1: Công bố và Ấn phẩm** (Publications)
- ✅ **Bài báo khoa học** (Journal Articles) ← ĐỒ ÁN TẬP TRUNG VÀO ĐÂY
- Sách chuyên khảo (Monograph)
- Giáo trình (Textbook)
- Sách tham khảo (Reference Book)
- Kỷ yếu hội thảo (Conference Proceedings)
- Báo cáo kiến nghị (Policy Brief)
- Báo cáo tổng kết đề tài

#### **Nhóm 2: Tài sản Trí tuệ** (Intellectual Property)
- Bằng độc quyền sáng chế (Patent)
- Giải pháp hữu ích (Utility Solution)
- Bảo hộ giống cây trồng
- Bảo hộ kiểu dáng công nghiệp
- Quyền tác giả (Copyright)

#### **Nhóm 3: Sản phẩm Kỹ thuật & Công nghệ**
- Vật liệu mới (New Materials)
- Mẫu vật/Chế phẩm (Specimens/Products)
- Thiết bị, máy móc (Equipment)
- Dây chuyền công nghệ (Production Line)
- Mô hình vật lý (Physical Models)

#### **Nhóm 4: Tiêu chuẩn & Quy phạm**
- Tiêu chuẩn Quốc gia (TCVN)
- Quy chuẩn Kỹ thuật Quốc gia (QCVN)
- Tiêu chuẩn cơ sở (TCCS)

#### **Nhóm 5: Thiết kế & Quy hoạch**
- Bản vẽ thiết kế thi công
- Đồ án quy hoạch
- Tác phẩm kiến trúc

#### **Nhóm 6: Dữ liệu & Số hóa**
- Phần mềm máy tính (Software)
- Cơ sở dữ liệu (Database)
- Bản đồ chuyên đề

#### **Nhóm 7: Đặc thù (Văn hóa - Nghệ thuật)**
- Tác phẩm nghệ thuật
- Chương trình biểu diễn

→ **Chi tiết đầy đủ**: Xem [research_output_catalog.md](./research_output_catalog.md)

---

### 1.3. Khung Pháp Lý Toàn Diện

Hệ thống quản lý TOÀN DIỆN phải tuân thủ 8 văn bản chính:

| Văn bản | Số hiệu | Phạm vi |
|---------|---------|---------|
| Luật KH, CN & ĐMST | 93/2025/QH15 | Nguyên tắc chung |
| Nghị định tài chính | 265/2025/NĐ-CP | Khoán chi, xử lý tài sản |
| Nghị định quản lý nhiệm vụ | 267/2025/NĐ-CP | Đánh giá nghiệm thu |
| Nghị định đơn giản hóa | 15/2026/NĐ-CP | Thủ tục hành chính |
| Thông tư quản lý cấp Bộ | 44/2025/TT-BKHCN | Đặt hàng, tuyển chọn |
| Thông tư chương trình QG | 36/2025/TT-BKHCN | Chương trình quốc gia |
| Thông tư cấp tỉnh | 09/2024/TT-BKHCN | Nhiệm vụ địa phương |
| Thông tư CSDL quốc gia | 11/2023/TT-BKHCN | Báo cáo, đăng ký |

→ **Chi tiết pháp lý**: Xem [legal_framework.md](./legal_framework.md)

---

### 1.4. Stakeholders Toàn Hệ Thống

**Cấp Quốc gia:**
- Bộ Khoa học và Công nghệ
- Quỹ Phát triển KH&CN Quốc gia
- Cục Thông tin KH&CN Quốc gia

**Cấp Bộ/Ngành:**
- 18 Bộ, ngành có hoạt động NCKH
- Các Quỹ phát triển KH&CN ngành

**Cấp Địa phương:**
- 63 Sở KH&CN tỉnh/thành
- Các trường Đại học, Viện nghiên cứu

**Người dùng cuối:**
- Nhà khoa học
- Cán bộ quản lý KH&CN
- Doanh nghiệp (tiếp nhận chuyển giao)
- Cộng đồng (thụ hưởng kết quả)

→ **Chi tiết stakeholders**: Xem [stakeholders_full.md](./stakeholders_full.md)

---

## 2. Vấn Đề Thực Tế (Problem Statement)

### 2.1. Tình Trạng Hiện Tại

**❌ Phân mảnh dữ liệu:**
- Mỗi trường ĐH/Viện có cách quản lý riêng (Excel, file giấy)
- Không thống nhất chuẩn dữ liệu
- Khó tổng hợp báo cáo quốc gia

**❌ Quy trình thủ công:**
- Nhập liệu trùng lặp nhiều lần
- Biểu mẫu giấy tờ phức tạp
- Thời gian báo cáo dài

**❌ Khó khăn tra cứu:**
- Không có hệ thống tìm kiếm tập trung
- Công trình bị "chôn vùi", không được sử dụng lại
- Khó đánh giá năng suất nghiên cứu

**❌ Không tuân thủ pháp luật:**
- Nhiều đơn vị chưa báo cáo kịp thời cho CSDL quốc gia
- Vi phạm Thông tư 11/2023 (báo cáo 30 ngày sau nghiệm thu)

---

### 2.2. Nhu Cầu Từ Các Bên

**Nhà nước:**
- Nắm bắt hiện trạng NCKH toàn quốc
- Định hướng đầu tư, tránh trùng lặp
- Đo lường hiệu quả ngân sách KH&CN

**Trường ĐH/Viện:**
- Quản lý hiệu quả công trình của đơn vị
- Đánh giá năng lực nghiên cứu giảng viên
- Hỗ trợ xếp hạng, kiểm định chất lượng

**Giảng viên/Nhà khoa học:**
- Dễ dàng đăng ký, cập nhật công trình
- Có hồ sơ nghiên cứu cá nhân (profile)
- Tăng khả năng hiển thị công trình

**Doanh nghiệp:**
- Tìm kiếm công nghệ để chuyển giao
- Kết nối với nhà khoa học

---

## 3. Giải Pháp Lý Tưởng (Toàn Diện)

### 3.1. Tầm Nhìn

> **"Hệ thống quốc gia thống nhất quản lý TOÀN BỘ 7 nhóm công trình NCKH, kết nối từ Bộ → Tỉnh → Cơ sở, hỗ trợ toàn bộ chu trình từ đặt hàng → nghiệm thu → thương mại hóa."**

### 3.2. Chức Năng Lý Tưởng

```
┌─────────────────────────────────────────┐
│  Quản lý Đầy Đủ 7 Nhóm Công Trình      │
├─────────────────────────────────────────┤
│  Tích hợp CSDL Quốc gia (real-time)    │
│  Tích hợp Cổng DVC Công                 │
│  Quản lý vòng đời đề tài (cradle-to-grave)│
│  Quản lý tài sản trí tuệ                │
│  Hỗ trợ thương mại hóa                  │
│  Báo cáo đa cấp (Bộ/Tỉnh/Cơ sở)       │
│  Tìm kiếm thông minh (AI)              │
│  Phân tích bibliometrics               │
└─────────────────────────────────────────┘
```

### 3.3. Quy Mô Lý Tưởng

- **Người dùng**: ~500,000 (tất cả nhà KH trong cả nước)
- **Cơ quan**: 63 tỉnh + 18 Bộ + 300+ trường ĐH/Viện
- **Dữ liệu**: Hàng triệu công trình tích lũy qua nhiều năm

---

## 4. Thách Thức Triển Khai Toàn Diện

### 4.1. Kỹ Thuật

- ⚠️ Quy mô lớn → cần kiến trúc phân tán, microservices
- ⚠️ Tích hợp nhiều hệ thống legacy khác nhau
- ⚠️ Đảm bảo hiệu năng với hàng triệu bản ghi

### 4.2. Tổ chức

- ⚠️ Cần sự phối hợp liên Bộ, liên ngành
- ⚠️ Đầu tư lớn về ngân sách, nhân lực
- ⚠️ Thời gian triển khai dài (5-10 năm)

### 4.3. Con Người

- ⚠️ Thay đổi thói quen làm việc của hàng trăm nghìn người
- ⚠️ Đào tạo, hỗ trợ trên diện rộng
- ⚠️ Kháng cự thay đổi

---

## 5. 🎯 Vị Trí của Đồ Án Này

### 5.1. Phạm Vi Đồ Án

Đồ án tập trung vào **1 module nhỏ nhưng cốt lõi**:

```
✅ Loại công trình: CHỈ Bài báo khoa học (Journal Articles)
✅ Đối tượng: CHỈ Giảng viên
✅ Cơ quan: CHỈ 1 Trường Đại học
✅ Chức năng: CRUD cơ bản + Tìm kiếm + Báo cáo đơn giản
```

### 5.2. Lý Do Chọn Phạm Vi Này

**1. Quan trọng nhất trong nghiên cứu:**
- Bài báo khoa học là chỉ tiêu KPI chính của giảng viên
- Ảnh hưởng trực tiếp đến xếp hạng trường ĐH
- Dễ định lượng (Web of Science, Scopus, Impact Factor)

**2. Dữ liệu tương đối chuẩn:**
- Có DOI, ISSN
- Có API từ ORCID, Crossref, Google Scholar
- Metadata đã được chuẩn hóa quốc tế

**3. Phù hợp quy mô đồ án:**
- Không quá phức tạp
- Có thể hoàn thiện trong thời gian học kỳ
- Vẫn đủ thử thách kỹ thuật

**4. Có thể mở rộng sau:**
- Module này là nền tảng
- Sau này có thể thêm các loại công trình khác
- Scalable architecture

---

### 5.3. Giá Trị Đóng Góp

Dù chỉ là module nhỏ, đồ án vẫn mang lại giá trị:

✅ **Cho giảng viên**: Quản lý hồ sơ nghiên cứu cá nhân  
✅ **Cho trường ĐH**: Theo dõi năng suất nghiên cứu  
✅ **Cho sinh viên**: Tìm hiểu hướng nghiên cứu của giảng viên  
✅ **Cho cộng đồng**: Khám phá kiến thức khoa học  

---

## 6. Kết Luận

**Toàn cảnh bài toán** (folder này) giúp:
- ✅ Hiểu bối cảnh lớn hơn
- ✅ Nhận thức được giá trị của module nhỏ trong hệ thống lớn
- ✅ Thiết kế với tư duy mở rộng được

**Đồ án thực tế** (folder 01-08) sẽ:
- ✅ Tập trung giải quyết 1 vấn đề cụ thể
- ✅ Hoàn thiện với chất lượng cao
- ✅ Là proof-of-concept cho hệ thống lớn hơn

---

## 📚 Các Tài Liệu Chi Tiết trong Folder Này

1. **[research_output_catalog.md](./research_output_catalog.md)** - Danh mục đầy đủ 7 nhóm, 28 loại công trình
2. **[legal_framework.md](./legal_framework.md)** - Phân tích chi tiết 8 văn bản pháp luật
3. **[stakeholders_full.md](./stakeholders_full.md)** - Tất cả các bên liên quan (quốc gia, ngành, cơ sở)
4. **[problem_context.md](./problem_context.md)** - Phân tích sâu vấn đề và giải pháp lý tưởng

---

*Folder này cung cấp **context**, không phải **requirements** cho đồ án. Requirements chi tiết nằm ở folder 01-08.*
