**YÊU CẦU BÀI TOÁN**

**Module: QUẢN LÝ CÔNG TRÌNH KHOA HỌC (BÀI BÁO KHOA HỌC)**

-----
**1. Mục tiêu**

Xây dựng module phần mềm hỗ trợ **quản lý công trình khoa học (bài báo khoa học)** của giảng viên trong trường đại học, cho phép:

- Giảng viên khai báo và nộp công trình
- Đơn vị quản lý xét duyệt theo **2 cấp: Khoa và Trường**
- Phản hồi yêu cầu bổ sung, chỉnh sửa
- Thống kê, báo cáo công trình khoa học
- Giảng viên theo dõi và xem kết quả xét duyệt

Module bao gồm **Frontend + Backend**, hoạt động theo mô hình **Web application**.

-----
**2. Đối tượng sử dụng và phân quyền**

**2.1. Giảng viên (GV)**

- Khai báo công trình khoa học
- Nộp hồ sơ xét duyệt
- Chỉnh sửa theo phản hồi
- Xem trạng thái và kết quả xét duyệt

**2.2. Cán bộ quản lý cấp Khoa**

- Xem danh sách công trình chờ duyệt
- Phê duyệt hoặc yêu cầu bổ sung
- Gửi công trình lên cấp Trường

**2.3. Cán bộ quản lý cấp Trường**

- Xem công trình đã được Khoa thông qua
- Phê duyệt cuối cùng hoặc từ chối
-----
**3. Yêu cầu chức năng Backend**

**3.1. Quản lý công trình khoa học**

Hệ thống phải cho phép:

- Tạo mới công trình khoa học
- Chỉnh sửa công trình (khi chưa được duyệt hoặc bị yêu cầu bổ sung)
- Lưu trữ thông tin công trình bao gồm:
  - Tên bài báo
  - Danh sách tác giả
  - Tạp chí/Hội nghị
  - Năm công bố
  - Loại chỉ mục (ISI/Scopus/Quốc gia/Khác)
  - File bài báo (PDF)
  - Trạng thái xử lý
-----
**3.2. Quản lý trạng thái công trình**

Mỗi công trình phải có trạng thái, bao gồm tối thiểu:

- Nháp (Draft)
- Đã nộp (Submitted)
- Yêu cầu bổ sung (Require Revision)
- Đã duyệt cấp Khoa
- Không duyệt cấp Khoa
- Đã duyệt cấp Trường
- Không duyệt cấp Trường

Hệ thống phải:

- Kiểm soát luồng chuyển trạng thái hợp lệ
- Lưu lịch sử xét duyệt và phản hồi
-----
**3.3. Phê duyệt và phản hồi**

Hệ thống phải cho phép:

- Cán bộ Khoa/Trường:
  - Xem chi tiết công trình
  - Tải file bài báo
  - Nhập nhận xét
  - Chọn quyết định:
    - Thông qua
    - Yêu cầu bổ sung
    - Không thông qua
- Lưu lại:
  - Người xét duyệt
  - Thời gian
  - Nội dung phản hồi
-----
**3.4. Thống kê và báo cáo**

Hệ thống phải hỗ trợ:

- Thống kê số lượng công trình theo:
  - Năm công bố
  - Khoa
  - Loại chỉ mục
  - Trạng thái
- Xuất báo cáo dưới dạng:
  - Bảng danh sách
  - File Excel hoặc PDF (nếu có)
-----
**4. Yêu cầu chức năng Frontend**

**4.1. Giao diện giảng viên**

Phải có các màn hình:

- Khai báo công trình khoa học (form nhập liệu + upload file)
- Danh sách công trình đã khai báo
- Xem chi tiết công trình:
  - Trạng thái hiện tại
  - Nhận xét của Khoa/Trường
- Chỉnh sửa và nộp lại khi bị yêu cầu bổ sung
-----
**4.2. Giao diện cán bộ cấp Khoa**

Phải có:

- Danh sách công trình chờ duyệt cấp Khoa
- Màn hình xem chi tiết công trình
- Chức năng:
  - Phê duyệt
  - Yêu cầu bổ sung
  - Không phê duyệt
-----
**4.3. Giao diện cán bộ cấp Trường**

Phải có:

- Danh sách công trình đã được Khoa duyệt
- Màn hình phê duyệt cuối cùng
- Ghi nhận quyết định và phản hồi
-----
**4.4. Giao diện thống kê – báo cáo**

- Bảng danh sách công trình
- Biểu đồ thống kê cơ bản
- Bộ lọc theo năm, khoa, trạng thái
-----
**5. Yêu cầu kỹ thuật**

- Backend:
  - RESTful API
  - Quản lý phân quyền theo vai trò
  - Lưu trữ dữ liệu trong CSDL
- Frontend:
  - Web-based
  - Phân biệt giao diện theo vai trò
- Bảo mật:
  - Người dùng chỉ xem/sửa dữ liệu đúng quyền

