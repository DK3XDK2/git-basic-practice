# BÁO CÁO KẾT QUẢ BÀI TẬP THỰC HÀNH GIT (BÀI 1 - BÀI 6)

- **Họ và tên:** Vũ Quang Huy
- **Email:** hacktyper12@gmail.com
- **GitHub Username:** DK3XDK2

---

## 🔗 LINK GITHUB REPOSITORY ĐỂ NỘP BÀI

1. **Repository Bài 1 - Bài 5 (git-basic-practice):**
   👉 **https://github.com/DK3XDK2/git-basic-practice**

2. **Repository Bài 6 - Dự án tổng hợp Portfolio (personal-portfolio):**
   👉 **https://github.com/DK3XDK2/personal-portfolio**

---

## BÀI 1: KHỞI TẠO REPOSITORY VÀ THỰC HIỆN COMMIT ĐẦU TIÊN

### 1. Thao tác thực hiện
- Khởi tạo thư mục `git-basic-practice` và chạy `git init -b main`.
- Tạo 3 file: `index.html`, `style.css`, `notes.txt`.
- Đưa `index.html` và `style.css` vào Staging Area bằng lệnh:
  ```bash
  git add index.html style.css
  ```
- Commit lần đầu với message: `"Initial commit: add html and css"`:
  ```bash
  git commit -m "Initial commit: add html and css"
  ```

### 2. Output minh chứng

#### a) Output `git status` trước khi commit:
```text
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   index.html
	new file:   style.css

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	notes.txt
```
*(Xác nhận: `index.html` và `style.css` nằm trong staging area; `notes.txt` vẫn ở trạng thái Untracked)*

#### b) Output `git status` sau khi commit:
```text
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	notes.txt

nothing added to commit but untracked files present (use "git add" to track)
```
*(Xác nhận: Sau commit, `notes.txt` vẫn ở trạng thái Untracked)*

#### c) Output `git log` sau khi commit đầu tiên:
```text
commit c41d4a20db3c10381912cd472c197217ec69c474
Author: Vu Quang Huy <hacktyper12@gmail.com>
Date:   Mon Sep 14 09:04:33 2026 +0700

    Initial commit: add html and css
```

### 3. Câu hỏi tư duy
> **Câu hỏi:** Staging area (Index) có vai trò gì mà nếu không có nó, việc commit sẽ bất tiện như thế nào?
>
> **Trả lời:**
> - **Vai trò của Staging Area:** Là vùng đệm (vùng chuẩn bị) trung gian giữa Working Directory (thư mục làm việc trên ổ đĩa) và Git Repository (kho lưu trữ lịch sử commit). Staging Area cho phép lập trình viên lựa chọn chính xác những file hoặc thậm chí từng đoạn code cụ thể (`git add -p`) để đóng gói thành một commit hoàn chỉnh, có ý nghĩa và mang tính nguyên tử (atomic commit).
> - **Sự bất tiện nếu không có Staging Area:**
>   1. **Không thể chia nhỏ các thay đổi:** Nếu đang làm nhiều việc cùng lúc (ví dụ vừa sửa lỗi bug A vừa phát triển tính năng B), ta bắt buộc phải commit toàn bộ mọi file đang chỉnh sửa trong 1 commit duy nhất, khiến commit message trở nên lộn xộn và khó kiểm soát.
>   2. **Dễ commit nhầm file rác / file tạm:** Các file nháp, file log, file cấu hình cá nhân hoặc các ghi chú như `notes.txt` sẽ vô tình bị đưa thẳng vào repo nếu không có bước chọn lọc qua staging area.
>   3. **Mất lớp kiểm duyệt an toàn:** Không thể dùng `git diff --staged` để rà soát kỹ lưỡng lần cuối những gì sắp được lưu trữ chính thức vào lịch sử dự án.

---

## BÀI 2: THỰC HÀNH GIT COMMIT NHIỀU LẦN VÀ XEM LỊCH SỬ

### 1. Thao tác thực hiện
1. Sửa `index.html` -> commit: `"Update html content"`.
2. Tạo file `script.js` -> add và commit: `"Add javascript file"`.
3. Sửa đồng thời `style.css` và `notes.txt` -> commit cùng lúc: `"Update style and notes"`.

### 2. Output minh chứng

#### a) Output `git log --oneline` (đủ 4 commit):
```text
1388461 Update style and notes
5d5555b Add javascript file
2c2c580 Update html content
c41d4a2 Initial commit: add html and css
```

#### b) Output `git show HEAD` (hoặc `git diff HEAD~1 HEAD`) xem chi tiết thay đổi commit gần nhất:
```diff
commit 13884613e30461fff56361bc288ef6ee79a3a986
Author: Vu Quang Huy <hacktyper12@gmail.com>
Date:   Mon Sep 14 09:04:58 2026 +0700

    Update style and notes

diff --git a/notes.txt b/notes.txt
new file mode 100644
index 0000000..c16e505
--- /dev/null
+++ b/notes.txt
@@ -0,0 +1,6 @@
+Ghi chú học tập Git:
+- Working Directory: Thư mục làm việc thực tế trên máy tính
+- Staging Area (Index): Vùng chuẩn bị các thay đổi trước khi commit
+- Repository: Nơi lưu trữ lịch sử và các commit chính thức
+- git commit: Lưu ảnh chụp trạng thái (snapshot) của Staging Area vào Repo
+- git diff: So sánh sự khác biệt giữa các phiên bản hoặc vùng làm việc
diff --git a/style.css b/style.css
index b5f138a..76f8666 100644
--- a/style.css
+++ b/style.css
@@ -3,8 +3,15 @@ body {
     margin: 40px;
     background-color: #f4f4f9;
     color: #333;
+    line-height: 1.6;
 }
 
 h1 {
     color: #2c3e50;
+    border-bottom: 2px solid #3498db;
+    padding-bottom: 10px;
+}
+
+p {
+    font-size: 16px;
 }
```

---

## BÀI 3: DI CHUYỂN GIỮA CÁC PHIÊN BẢN (CHECKOUT / RESET)

### 1. Thao tác thực hiện
1. Lấy hash của commit `"Add javascript file"`: `5d5555b`.
2. Chạy `git checkout 5d5555b` để chuyển sang chế độ **detached HEAD**:
   - Kiểm tra `script.js`: File tồn tại với nội dung đầy đủ.
   - Kiểm tra `notes.txt`: File **chưa hề tồn tại** (kết quả `Test-Path` là `False`) vì `notes.txt` chỉ được đưa vào repo ở commit sau (`1388461`).
3. Quay trở lại nhánh chính: `git checkout main`.
4. Thử nghiệm 3 loại reset với commit test chứa file `temp.txt`.

### 2. Bảng so sánh 3 loại Git Reset

| Lệnh Reset | Repository (Commit History / HEAD) | Staging Area (Index) | Working Directory (Thư mục làm việc) | Nhận xét trạng thái file `temp.txt` |
| :--- | :--- | :--- | :--- | :--- |
| **`git reset --soft HEAD~1`** | **Lùi lại 1 commit** (xóa commit khỏi branch) | **Giữ nguyên** các file đã stage của commit bị reset | **Giữ nguyên**, không mất dữ liệu | File `temp.txt` vẫn còn và ở trạng thái **staged** (`Changes to be committed`), sẵn sàng commit lại ngay. |
| **`git reset --mixed HEAD~1`** *(Mặc định)* | **Lùi lại 1 commit** (xóa commit khỏi branch) | **Bị reset** (unstage toàn bộ các file) | **Giữ nguyên**, không mất dữ liệu | File `temp.txt` vẫn còn nguyên nhưng ở trạng thái **untracked / unstaged**, cần `git add` lại nếu muốn commit. |
| **`git reset --hard HEAD~1`** | **Lùi lại 1 commit** (xóa commit khỏi branch) | **Bị reset sạch sẽ** | **Bị xóa bỏ hoàn toàn** mọi thay đổi của commit đó | File `temp.txt` **bị xóa vĩnh viễn** khỏi ổ đĩa, Working Directory sạch hoàn toàn. |

### 3. Output minh chứng các bước Reset

#### a) `git reset --soft HEAD~1`:
```text
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	new file:   temp.txt
```

#### b) `git reset --mixed HEAD~1`:
```text
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	temp.txt

nothing added to commit but untracked files present (use "git add" to track)
```

#### c) `git reset --hard HEAD~1`:
```text
HEAD is now at 1388461 Update style and notes
On branch main
nothing to commit, working tree clean
```
*(Kiểm tra `Test-Path temp.txt` trả về `False` - file đã bị xóa sạch)*

### 4. Câu hỏi tư duy
> **Câu hỏi:** Nếu đã push code lên GitHub cho cả team dùng, việc dùng `git reset --hard` để lùi lại commit có an toàn không? Vì sao?
>
> **Trả lời:**
> **Hoàn toàn KHÔNG AN TOÀN và RẤT NGUY HIỂM** trong môi trường làm việc nhóm vì các lý do sau:
> 1. **Ghi đè lịch sử công khai (Rewriting Public History):** Khi đã push commit lên remote repository, việc dùng `reset --hard` sẽ làm mất commit ở local. Để đồng bộ lên GitHub, người dùng buộc phải sử dụng cờ ép buộc (`git push --force`). Thao tác này sẽ ghi đè lịch sử chung trên GitHub.
> 2. **Gây xung đột và lỗi đồng bộ cho các thành viên khác:** Các thành viên trong team đã pull commit đó về máy của họ. Khi branch trên remote bị ép lùi lại, lịch sử giữa local của họ và remote sẽ bị lệch nhánh (diverged branches). Khi họ `pull` hoặc `push`, Git sẽ báo lỗi, sinh ra các merge conflict phức tạp hoặc commit bị xóa lại vô tình bị merge ngược trở lại repo.
> 3. **Nguy cơ mất trắng code:** Mọi thay đổi chưa kịp sao lưu hoặc những đoạn code bị reset mà không ai giữ bản sao sẽ bị mất hoàn toàn.
>
> **Giải pháp chuẩn:** Khi code đã push lên GitHub, luôn dùng **`git revert <commit-hash>`**. Lệnh này sẽ tạo ra một commit mới để đảo ngược thay đổi của commit lỗi, giữ nguyên toàn vẹn chuỗi lịch sử và an toàn tuyệt đối cho cả nhóm.

---

## BÀI 4: TẠO PROJECT MỚI TRÊN GITHUB VÀ KẾT NỐI REMOTE

### 1. Thao tác thực hiện
- Tạo repository `git-basic-practice` trên GitHub (chế độ Public, không tick README).
- Kết nối remote `origin`:
  ```bash
  git remote add origin https://github.com/DK3XDK2/git-basic-practice.git
  ```
- Kiểm tra remote: `git remote -v`.
- Đẩy toàn bộ lịch sử lên GitHub:
  ```bash
  git push -u origin main
  ```

### 2. Output minh chứng

#### a) Output `git remote -v`:
```text
origin	https://github.com/DK3XDK2/git-basic-practice.git (fetch)
origin	https://github.com/DK3XDK2/git-basic-practice.git (push)
```

#### b) Output `git push -u origin main`:
```text
branch 'main' set up to track 'origin/main'.
To https://github.com/DK3XDK2/git-basic-practice.git
 * [new branch]      main -> main
```

#### c) Link GitHub repository:
👉 **https://github.com/DK3XDK2/git-basic-practice**

---

## BÀI 5: ĐỒNG BỘ REMOTE REPOSITORY (CLONE / PULL / PUSH)

### 1. Thao tác thực hiện
1. **Clone dự án:** Clone `git-basic-practice` sang thư mục mới `git-sample-clone`, kiểm tra `git remote -v` và `git log --oneline`.
2. **Push từ local:** Tạo file `about.txt` trên `git-basic-practice`, commit với message `"Add about.txt"` và `git push origin main`.
3. **Giả lập commit trên GitHub:** Tạo file `README.md` với commit `"Create README.md via GitHub Web interface"`.
4. **Pull về máy local:** Chạy `git pull origin main`.

### 2. Output minh chứng

#### a) Log trước khi pull:
```text
=== LOG TRUOC KHI PULL ===
51f53e9 Add about.txt
1388461 Update style and notes
5d5555b Add javascript file
```

#### b) Thực hiện lệnh `git pull origin main`:
```text
From https://github.com/DK3XDK2/git-basic-practice
 * branch            main       -> FETCH_HEAD
   51f53e9..fdb7c8b  main       -> origin/main
Updating 51f53e9..fdb7c8b
Fast-forward
 README.md | 10 ++++++++++
 1 file changed, 10 insertions(+)
 create mode 100644 README.md
```

#### c) Log sau khi pull (commit mới từ GitHub đã xuất hiện):
```text
=== LOG SAU KHI PULL ===
fdb7c8b Create README.md via GitHub Web interface
51f53e9 Add about.txt
1388461 Update style and notes
5d5555b Add javascript file
```

### 3. Trả lời câu hỏi
> **Câu hỏi:** `git pull` thực chất là tổ hợp của 2 lệnh nào?
>
> **Trả lời:**
> Lệnh `git pull` thực chất là tổ hợp chạy tuần tự của 2 lệnh:
> 1. **`git fetch`**: Liên lạc với remote repository để tải về tất cả các commit, branch, tag mới nhất về local repository (nhưng chưa tác động vào Working Directory hay file code đang mở).
> 2. **`git merge`**: Tự động tích hợp (gộp) các commit vừa fetch từ remote branch vào branch hiện tại trên local máy làm việc (nếu cấu hình `--rebase` thì sẽ là `git fetch` + `git rebase`).

---

## BÀI 6 (TỔNG HỢP): MÔ PHỎNG QUY TRÌNH LÀM VIỆC HOÀN CHỈNH

### 1. Thao tác thực hiện
Dự án được xây dựng trong repo `personal-portfolio`:
1. Khởi tạo repository local, tạo cấu trúc file ban đầu (`index.html`, `style.css`) -> Commit: `"Initial structure"`.
2. Tạo repo `personal-portfolio` trên GitHub -> kết nối remote `origin` -> Push commit đầu tiên lên GitHub.
3. Bổ sung mục "Giới thiệu bản thân" vào `index.html` -> Commit: `"Add introduction section"` -> Push lên GitHub.
4. Thêm style CSS đẹp mắt cho phần giới thiệu -> Commit: `"Style introduction section"` -> Push lên GitHub.
5. Cố tình sửa sai CSS làm hỏng giao diện -> Commit: `"Wrong css: break layout and colors"` -> Push lên GitHub.
6. Sử dụng **`git revert HEAD --no-edit`** để hoàn tác commit hỏng mà không làm mất các commit trước đó -> Commit revert tự động được tạo -> Push lên GitHub.

### 2. Output minh chứng lịch sử commit trên GitHub

Output `git log --oneline` thể hiện rõ toàn bộ quá trình:
```text
0fdfb33 Revert "Wrong css: break layout and colors"
43d250f Wrong css: break layout and colors
220af49 Style introduction section
c750598 Add introduction section
229728d Initial structure
```

### 3. Link GitHub repository Bài 6
👉 **https://github.com/DK3XDK2/personal-portfolio**
