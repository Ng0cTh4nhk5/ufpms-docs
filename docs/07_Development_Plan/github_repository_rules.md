# Hướng Dẫn Setup GitHub Repository Rules - UFPMS V1.0

> 📅 **Cập nhật**: 19/02/2026
> 🎯 **Mục tiêu**: Đảm bảo quy trình code an toàn, chất lượng và đồng bộ giữa Frontend & Backend.
> ⚠️ **Áp dụng cho**: Cả 2 repositories `ufpms-backend` và `ufpms-frontend`.

---

## 1. Cấu Trúc Nhánh (Branch Strategy)

Chúng ta sử dụng **GitFlow Lite**:

- **`main`**: Nhánh Production. Code ổn định, sẵn sàng deploy. **CẤM push trực tiếp**.
- **`develop`**: Nhánh Staging/Integration. Nơi merge các tính năng mới. **CẤM push trực tiếp**.
- **`feature/*`**: Nhánh chức năng (VD: `feature/login-page`). Tạo từ `develop`, merge vào `develop`.
- **`bugfix/*`**: Nhánh sửa lỗi.
- **`release/*`**: Nhánh chuẩn bị release (nếu cần).

---

## 2. Thiết Lập Branch Protection Rules

Để bảo vệ code, bạn cần thiết lập **Rules** trên GitHub cho 2 nhánh chính: `main` và `develop`.

### ✅ Rule 1: Bảo Vệ Nhánh `main` (Production)

**Mục đích**: Đảm bảo code trên `main` luôn chạy tốt, đã được test kỹ.

1. Vào **Settings** của repository.
2. Chọn menu **Branches** (hoặc **Code and automation** → **Branches**).
3. Nhấn **Add branch protection rule**.
4. **Branch name pattern**: `main`
5. Tích chọn các mục sau:
   - [x] **Require a pull request before merging**
     - [x] **Require approvals**: `1` (Tối thiểu 1 người review)
     - [x] **Dismiss stale pull request approvals when new commits are pushed** (Bắt review lại nếu có code mới đẩy lên PR)
   - [x] **Require status checks to pass before merging** (Bắt buộc CI/CD build thành công mới được merge)
     - *Lưu ý quan trọng*: Ban đầu mục này sẽ trống. Bạn cần setup và chạy CI/CD (GitHub Actions) thành công ít nhất 1 lần thì tên job (ví dụ: `build-and-test`) mới hiện ra ở đây để bạn tìm kiếm và tích chọn.
   - [x] **Require linear history** (Bắt buộc, giúp lịch sử commit thẳng hàng, dễ theo dõi)
   - [x] **Include administrators** (Admin cũng phải tuân thủ, không được bypass)
   - [x] **Restrict deletions** (Không ai được xóa nhánh main)
6. Nhấn **Create** / **Save changes**.

---

### ✅ Rule 2: Bảo Vệ Nhánh `develop` (Staging)

**Mục đích**: Đảm bảo code tích hợp không bị lỗi build cơ bản, nhưng linh hoạt hơn `main`.

1. Nhấn **Add branch protection rule** lần nữa.
2. **Branch name pattern**: `develop`
3. Tích chọn các mục sau:
   - [x] **Require a pull request before merging**
     - [x] **Require approvals**: `1`
   - [x] **Require status checks to pass before merging**
   - [x] **Include administrators**
   - [x] **Restrict deletions**
   - [ ] *Không cần tích **Require linear history** (để merge commit cho dễ nhìn các cụm tính năng)*
4. Nhấn **Create** / **Save changes**.

---

## 3. Quy Tắc Merge & Commit

### 📝 Commit Message Convention
Theo chuẩn [Conventional Commits](https://www.conventionalcommits.org/):

- `feat: ...`: Tính năng mới
- `fix: ...`: Sửa lỗi
- `docs: ...`: Thay đổi tài liệu
- `style: ...`: Format code, dấu chấm phẩy... (không đổi logic)
- `refactor: ...`: Sửa code nhưng không đổi tính năng/fix bug
- `test: ...`: Thêm/sửa test
- `chore: ...`: Update build tasks, dependencies...

**Ví dụ**:
- `feat(auth): add login api endpoint`
- `fix(ui): resolve button alignment issue on mobile`

### 🔀 Quy Trình Merge (Pull Request)

1. **Dev** tạo Pull Request (PR) từ `feature/...` vào `develop`.
2. **CI/CD** tự động chạy (Build & Test).
3. **Reviewer** (Tech Lead hoặc Dev khác) vào review code:
   - Kiểm tra logic, coding convention.
   - Comment yêu cầu sửa (Change requested) hoặc Approve.
4. Sau khi `Approve` + `CI Passed` → Nút **Merge** sẽ hiện xanh.
5. **Dev** nhấn Merge (chọn **Squash and merge** để gộp commit cho gọn, hoặc **Create a merge commit**).

---

## 4. Kiểm Tra Setup

Sau khi setup xong, hãy thử:
1. `git checkout main`
2. Sửa 1 file bất kỳ.
3. `git push origin main`

🛑 **Kết quả mong đợi**: Git báo lỗi (rejected) và yêu cầu tạo Pull Request.
👉 **Thành công!** Code của bạn đã được bảo vệ an toàn.
