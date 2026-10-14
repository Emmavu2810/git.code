# Git / GitHub Command Cheat Sheet

> Bảng tra cứu nhanh các lệnh Git thường dùng khi làm việc với GitHub.\
> **Git** quản lý phiên bản trên máy tính; **GitHub** lưu repository
> trực tuyến và hỗ trợ cộng tác.

## 1. Cấu hình ban đầu

  ----------------------------------------------------------------------------------------
  Lệnh                                                 Công dụng
  ---------------------------------------------------- -----------------------------------
  `git --version`                                      Kiểm tra Git đã được cài đặt chưa

  `git config --global user.name "Your Name"`          Cấu hình tên người commit

  `git config --global user.email "you@example.com"`   Cấu hình email commit

  `git config --global --list`                         Xem cấu hình Git hiện tại
  ----------------------------------------------------------------------------------------

## 2. Tạo hoặc tải repository

  -----------------------------------------------------------------------
  Lệnh                                Công dụng
  ----------------------------------- -----------------------------------
  `git init`                          Khởi tạo repository Git trong thư
                                      mục hiện tại

  `git clone <URL>`                   Tải repository từ GitHub về máy

  `git remote -v`                     Xem các remote đã cấu hình

  `git remote add origin <URL>`       Kết nối repository local với remote
                                      tên `origin`

  `git remote set-url origin <URL>`   Thay đổi URL của remote `origin`
  -----------------------------------------------------------------------

Ví dụ:

``` bash
git clone https://github.com/USERNAME/REPOSITORY.git
cd REPOSITORY
```

## 3. Kiểm tra thay đổi và lưu phiên bản

  Lệnh                        Công dụng
  --------------------------- -------------------------------------------
  `git status`                Xem trạng thái file
  `git diff`                  Xem thay đổi chưa được stage
  `git diff --staged`         Xem thay đổi đã stage
  `git add <file>`            Stage một file cụ thể
  `git add .`                 Stage các thay đổi trong thư mục hiện tại
  `git commit -m "message"`   Tạo commit từ các thay đổi đã stage
  `git log --oneline`         Xem lịch sử commit dạng ngắn

Quy trình cơ bản:

``` bash
git status
git add .
git commit -m "Describe your changes"
```

## 4. Đồng bộ với GitHub

  -----------------------------------------------------------------------
  Lệnh                                Công dụng
  ----------------------------------- -----------------------------------
  `git fetch`                         Tải thông tin mới từ remote nhưng
                                      chưa tích hợp vào nhánh hiện tại

  `git pull`                          Lấy và tích hợp thay đổi từ remote
                                      vào nhánh hiện tại

  `git push`                          Đẩy commit lên remote

  `git push -u origin main`           Đẩy nhánh `main` lần đầu và thiết
                                      lập upstream

  `git pull origin main`              Lấy thay đổi từ nhánh `main` trên
                                      remote
  -----------------------------------------------------------------------

Ví dụ quy trình cập nhật:

``` bash
git add .
git commit -m "Update documentation"
git push
```

## 5. Làm việc với branch

  ------------------------------------------------------------------------
  Lệnh                                 Công dụng
  ------------------------------------ -----------------------------------
  `git branch`                         Liệt kê các branch local

  `git branch <branch-name>`           Tạo branch mới

  `git switch <branch-name>`           Chuyển sang branch có sẵn

  `git switch -c <branch-name>`        Tạo và chuyển sang branch mới

  `git merge <branch-name>`            Gộp branch được chỉ định vào branch
                                       hiện tại

  `git branch -d <branch-name>`        Xóa branch local đã được gộp

  `git push -u origin <branch-name>`   Đẩy branch mới lên GitHub
  ------------------------------------------------------------------------

Ví dụ tạo branch để làm một task:

``` bash
git switch -c feature/update-readme
# Chỉnh sửa file...
git add .
git commit -m "Update README"
git push -u origin feature/update-readme
```

Sau đó, mở GitHub và tạo **Pull Request (PR)** để đề xuất gộp thay đổi.

## 6. Khôi phục thay đổi --- dùng cẩn thận

  ---------------------------------------------------------------------------
  Lệnh                                    Công dụng / Lưu ý
  --------------------------------------- -----------------------------------
  `git restore <file>`                    Bỏ thay đổi chưa stage của file;
                                          thay đổi bị bỏ có thể mất

  `git restore --staged <file>`           Bỏ stage file, nhưng giữ nội dung
                                          đã chỉnh sửa

  `git commit --amend -m "New message"`   Sửa commit gần nhất; tránh dùng với
                                          commit đã chia sẻ nếu chưa hiểu hệ
                                          quả

  `git revert <commit-id>`                Tạo commit mới để đảo ngược một
                                          commit trước đó

  `git stash`                             Tạm cất các thay đổi chưa commit

  `git stash pop`                         Lấy thay đổi gần nhất từ stash và
                                          áp dụng lại
  ---------------------------------------------------------------------------

**Cẩn thận:** Trước khi chạy lệnh khôi phục hoặc xóa, hãy dùng
`git status` và kiểm tra xem có thay đổi nào cần giữ lại không.

## 7. Giải quyết xung đột (merge conflict)

1.  Chạy `git status` để xác định file đang xung đột.
2.  Mở file và tìm các dấu đánh dấu xung đột:

``` text
<<<<<<< HEAD
Nội dung trên branch hiện tại
=======
Nội dung từ branch được gộp
>>>>>>> other-branch
```

3.  Chỉnh sửa để giữ nội dung mong muốn và xóa các dấu đánh dấu.
4.  Đánh dấu đã giải quyết rồi commit:

``` bash
git add <file>
git commit -m "Resolve merge conflict"
```

## 8. Lệnh GitHub thường gặp trong quy trình cộng tác

  Thuật ngữ / thao tác    Ý nghĩa
  ----------------------- -------------------------------------------------------
  **Repository (repo)**   Nơi lưu code, tài liệu và lịch sử phiên bản
  **Fork**                Tạo bản sao repository trên tài khoản GitHub của mình
  **Clone**               Tải repository về máy tính
  **Commit**              Ghi lại một nhóm thay đổi trong lịch sử
  **Branch**              Nhánh làm việc độc lập
  **Push**                Đẩy commit từ máy lên remote
  **Pull**                Lấy và tích hợp thay đổi từ remote
  **Pull Request (PR)**   Đề xuất xem xét và gộp thay đổi
  **Issue**               Theo dõi lỗi, công việc hoặc đề xuất
  **README.md**           Tài liệu giới thiệu repository
  **`.gitignore`**        Khai báo file/thư mục Git không nên theo dõi

## 9. Quy trình mẫu: cập nhật một file và đẩy lên GitHub

``` bash
# 1. Đi vào thư mục dự án
cd <project-folder>

# 2. Kiểm tra trạng thái
git status

# 3. Lấy thay đổi mới nhất (nếu đang làm việc với remote)
git pull

# 4. Stage file cần cập nhật
git add <file-name>

# 5. Tạo commit
git commit -m "Update learning notes"

# 6. Đẩy lên GitHub
git push
```

Nếu đây là lần đầu đẩy một nhánh mới, dùng:

``` bash
git push -u origin <branch-name>
```

## 10. Các lỗi thường gặp

  -----------------------------------------------------------------------
  Tình huống                          Cách kiểm tra / xử lý
  ----------------------------------- -----------------------------------
  `nothing to commit`                 Chạy `git status`; có thể chưa có
                                      thay đổi hoặc chưa stage file

  `rejected` khi push                 Remote có commit mới; kiểm tra
                                      trạng thái và đồng bộ bằng
                                      `git pull` trước khi push lại

  `not a git repository`              Kiểm tra bạn đã đứng đúng thư mục
                                      repository chưa

  Sai remote URL                      Dùng `git remote -v`, rồi sửa bằng
                                      `git remote set-url origin <URL>`

  Quên branch hiện tại                Dùng `git branch --show-current`

  Muốn xem commit gần nhất            Dùng `git log -1 --oneline`
  -----------------------------------------------------------------------

## Ghi nhớ nhanh

``` text
git status                 # Kiểm tra trạng thái
git add .                  # Stage thay đổi
git commit -m "message"    # Tạo commit
git pull                   # Đồng bộ từ remote
git push                   # Đẩy lên remote
```

**Mẹo:** Chạy `git status` thường xuyên. Nó giúp bạn biết đang ở branch
nào, file nào đã thay đổi và bước tiếp theo nên làm gì.
