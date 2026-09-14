# BÁO CÁO BÀI TẬP THỰC HÀNH GIT

- Sinh viên: Vũ Quang Huy
- Email: hacktyper12@gmail.com
- GitHub Username: DK3XDK2

---

## Danh sách link repository nộp bài

- Repository Bài 1 đến Bài 5: https://github.com/DK3XDK2/git-basic-practice
- Repository Bài 6 (Dự án Portfolio): https://github.com/DK3XDK2/personal-portfolio

---

## Bài 1: Khởi tạo Repository và thực hiện commit đầu tiên

### 1. Quá trình thực hiện
- Tạo thư mục `git-basic-practice` và chạy lệnh `git init -b main` để khởi tạo kho chứa Git với nhánh chính là `main`.
- Tạo 3 file trong thư mục: `index.html`, `style.css` và `notes.txt`.
- Dùng lệnh `git status` kiểm tra, thấy cả 3 file đều đang ở trạng thái `Untracked files`.
- Thực hiện thêm 2 file `index.html` và `style.css` vào staging area bằng lệnh `git add index.html style.css`, để lại file `notes.txt`.
- Tiến hành commit đầu tiên bằng lệnh:
  `git commit -m "Initial commit: add html and css"`
- Sau khi commit, kiểm tra lại trạng thái bằng `git status` để đảm bảo file `notes.txt` vẫn chưa được theo dõi (untracked).

### 2. Kết quả terminal

Lệnh `git status` trước khi commit (2 file đã vào staging, notes.txt vẫn untracked):
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

Lệnh `git status` sau khi commit:
```text
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	notes.txt

nothing added to commit but untracked files present (use "git add" to track)
```

Lệnh `git log` xác nhận commit đầu tiên:
```text
commit c41d4a20db3c10381912cd472c197217ec69c474
Author: Vu Quang Huy <hacktyper12@gmail.com>
Date:   Mon Sep 14 09:04:33 2026 +0700

    Initial commit: add html and css
```

### 3. Trả lời câu hỏi tư duy
**Câu hỏi:** Staging area (Index) có vai trò gì mà nếu không có nó, việc commit sẽ bất tiện như thế nào?

**Trả lời:**
Staging area đóng vai trò là một vùng chuẩn bị trung gian giữa thư mục làm việc (Working Directory) và lịch sử lưu trữ (Repository). Nhờ có Staging area, người dùng có thể chọn lọc chính xác từng file hoặc từng dòng code cụ thể để đóng gói thành một commit hoàn chỉnh, mang đúng ý nghĩa của một lần cập nhật.

Nếu không có Staging area, mọi việc commit sẽ rất bất tiện:
- Khi đang làm dở nhiều việc cùng lúc (ví dụ vừa sửa một lỗi nhỏ, vừa phát triển dở một tính năng mới), ta sẽ buộc phải commit toàn bộ tất cả các file đã chỉnh sửa vào chung một commit. Điều này khiến lịch sử commit bị trộn lẫn và khó theo dõi.
- Các file tạm, file nháp cá nhân (như file `notes.txt` ở trên) hoặc các file cấu hình local rất dễ bị commit nhầm lên repository do không có bước lọc trước.
- Không thể kiểm tra trước những nội dung cụ thể sắp được ghi vào kho (bằng lệnh `git diff --staged`) trước khi xác nhận commit.

---

## Bài 2: Thực hành git commit nhiều lần và xem lịch sử

### 1. Quá trình thực hiện
- Chỉnh sửa nội dung file `index.html`, thêm một đoạn văn bản mới rồi commit với nội dung: `"Update html content"`.
- Tạo thêm file mã nguồn `script.js`, đưa vào staging area và commit với message: `"Add javascript file"`.
- Chỉnh sửa đồng thời cả 2 file `style.css` và `notes.txt`, sau đó thêm cả hai vào staging area và commit chung một lần với message: `"Update style and notes"`.
- Dùng `git log --oneline` để xem tóm tắt lịch sử 4 commit.
- Dùng `git show HEAD` để xem chi tiết thay đổi (diff) của lần commit gần nhất.

### 2. Kết quả terminal

Lệnh `git log --oneline` hiển thị đủ 4 commit:
```text
1388461 Update style and notes
5d5555b Add javascript file
2c2c580 Update html content
c41d4a2 Initial commit: add html and css
```

Lệnh `git show HEAD` hiển thị chi tiết thay đổi của commit mới nhất:
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

## Bài 3: Di chuyển giữa các phiên bản (checkout/reset)

### 1. Quá trình thực hiện
- Lấy mã hash của commit thứ 2 tính theo chiều tạo file ("Add javascript file"): mã hash là `5d5555b`.
- Dùng lệnh `git checkout 5d5555b` để chuyển trạng thái làm việc về thời điểm đó (detached HEAD).
  - Quan sát: File `script.js` đã tồn tại trong thư mục.
  - File `notes.txt` chưa xuất hiện, do ở thời điểm commit `5d5555b` file này vẫn chưa được commit vào repository.
- Quay trở lại nhánh chính bằng lệnh `git checkout main`. File `notes.txt` lại xuất hiện bình thường.
- Tạo một commit thử nghiệm chứa file `temp.txt` để kiểm tra lần lượt 3 chế độ reset (`--soft`, `--mixed`, `--hard`).

### 2. Bảng so sánh 3 chế độ Git Reset

| Chế độ Reset | Tác động lên Repository | Tác động lên Staging Area | Tác động lên Working Directory | Tình trạng file test `temp.txt` |
| :--- | :--- | :--- | :--- | :--- |
| **git reset --soft HEAD~1** | Lùi con trỏ HEAD về 1 commit trước đó | Giữ nguyên các file đã stage | Giữ nguyên các thay đổi trong file | File vẫn tồn tại và nằm sẵn trong staging area (`Changes to be committed`), có thể commit lại ngay lập tức. |
| **git reset --mixed HEAD~1** *(mặc định)* | Lùi con trỏ HEAD về 1 commit trước đó | Bị reset sạch (unstage các file) | Giữ nguyên nội dung các file trên đĩa | File vẫn còn trên ổ đĩa nhưng ở trạng thái chưa được theo dõi (`Untracked`), cần `git add` lại nếu muốn commit. |
| **git reset --hard HEAD~1** | Lùi con trỏ HEAD về 1 commit trước đó | Bị reset sạch | Bị xóa bỏ hoàn toàn các thay đổi của commit đó | File bị xóa hẳn khỏi thư mục làm việc, mã nguồn quay về nguyên vẹn như commit trước. |

### 3. Kết quả terminal từng bước reset

Khi chạy `git reset --soft HEAD~1`:
```text
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	new file:   temp.txt
```

Khi chạy `git reset --mixed HEAD~1`:
```text
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	temp.txt

nothing added to commit but untracked files present (use "git add" to track)
```

Khi chạy `git reset --hard HEAD~1`:
```text
HEAD is now at 1388461 Update style and notes
On branch main
nothing to commit, working tree clean
```
Kiểm tra lại sự tồn tại của file `temp.txt` trên ổ đĩa trả về kết quả không tìm thấy file.

### 4. Trả lời câu hỏi tư duy
**Câu hỏi:** Nếu đã push code lên GitHub cho cả team dùng, việc dùng `git reset --hard` để lùi lại commit có an toàn không? Vì sao?

**Trả lời:**
Thao tác này hoàn toàn **không an toàn** và bị xem là điều tối kỵ khi làm việc nhóm.
- Khi một commit đã được đẩy lên GitHub, các thành viên khác có thể đã kéo (pull) commit đó về máy của họ.
- Nếu một người tự ý dùng `git reset --hard` ở máy cá nhân rồi dùng lệnh `git push --force` để ghi đè lên GitHub, lịch sử trên máy chủ sẽ bị tua ngược, làm lệch lịch sử (diverged branches) giữa máy các thành viên và kho chung.
- Khi các thành viên khác tiếp tục đẩy hoặc kéo code, hệ thống sẽ báo lỗi xung đột hoặc các commit cũ bị xóa lại vô tình bị merge ngược trở lại, rất dễ gây mất code của đồng đội.
- Trong trường hợp code đã public trên GitHub, giải pháp an toàn là dùng lệnh `git revert <commit-hash>`. Lệnh này sẽ tạo ra một commit mới có nội dung đảo ngược lại commit lỗi mà vẫn giữ nguyên vẹn toàn bộ chuỗi lịch sử commit.

---

## Bài 4: Tạo project mới trên GitHub và kết nối remote

### 1. Quá trình thực hiện
- Truy cập GitHub tạo một repository mới tên là `git-basic-practice`, để chế độ Public và không tích chọn khởi tạo file README.
- Tại terminal của project trên máy, gán remote origin bằng lệnh:
  `git remote add origin https://github.com/DK3XDK2/git-basic-practice.git`
- Kiểm tra lại danh sách remote bằng `git remote -v`.
- Đẩy toàn bộ nhánh `main` lên GitHub và thiết lập tracking bằng lệnh:
  `git push -u origin main`

### 2. Kết quả terminal

Kiểm tra remote:
```text
origin	https://github.com/DK3XDK2/git-basic-practice.git (fetch)
origin	https://github.com/DK3XDK2/git-basic-practice.git (push)
```

Kết quả push lên GitHub:
```text
branch 'main' set up to track 'origin/main'.
To https://github.com/DK3XDK2/git-basic-practice.git
 * [new branch]      main -> main
```

Đường link repository: https://github.com/DK3XDK2/git-basic-practice

---

## Bài 5: Đồng bộ remote repository (clone/pull/push)

### 1. Quá trình thực hiện
- Thực hành clone repository về một thư mục riêng (`git-sample-clone`) để kiểm tra remote mặc định và xem lịch sử commit.
- Trên thư mục dự án chính, tạo thêm file `about.txt`, tiến hành commit với nội dung `"Add about.txt"` và push lên GitHub bằng `git push origin main`.
- Giả lập tình huống có commit từ nơi khác: tạo file `README.md` trực tiếp trên GitHub với commit message `"Create README.md via GitHub Web interface"`.
- Quay lại máy local, chạy lệnh `git pull origin main` để lấy file `README.md` mới về máy.

### 2. Kết quả terminal

Lịch sử commit tại local trước khi pull:
```text
51f53e9 Add about.txt
1388461 Update style and notes
5d5555b Add javascript file
```

Thực hiện lệnh `git pull origin main`:
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

Lịch sử commit sau khi pull (commit từ GitHub đã được tích hợp vào local):
```text
fdb7c8b Create README.md via GitHub Web interface
51f53e9 Add about.txt
1388461 Update style and notes
5d5555b Add javascript file
```

### 3. Trả lời câu hỏi
**Câu hỏi:** `git pull` thực chất là tổ hợp của 2 lệnh nào?

**Trả lời:**
Lệnh `git pull` thực chất là sự kết hợp tuần tự của 2 lệnh:
1. `git fetch`: Tải tất cả các nhánh, tag và commit mới nhất từ máy chủ GitHub về kho lưu trữ local (nhưng chưa can thiệp vào mã nguồn trên thư mục làm việc).
2. `git merge`: Tự động gộp (merge) nhánh vừa tải về từ remote vào nhánh local đang mở.

---

## Bài 6 (Tổng hợp): Mô phỏng quy trình làm việc hoàn chỉnh

### 1. Quá trình thực hiện
Tạo dự án trang giới thiệu cá nhân đơn giản tại repository riêng `personal-portfolio` với các bước tuần tự:
1. Khởi tạo repository local, tạo khung ban đầu cho file `index.html` và `style.css` rồi commit: `"Initial structure"`.
2. Tạo repository `personal-portfolio` trên GitHub, kết nối remote và push commit đầu tiên.
3. Bổ sung thẻ nội dung giới thiệu bản thân vào `index.html` rồi commit: `"Add introduction section"`, sau đó push lên GitHub.
4. Viết bổ sung CSS trang trí cho phần giới thiệu vừa tạo rồi commit: `"Style introduction section"`, sau đó push lên GitHub.
5. Cố tình sửa sai một đoạn mã CSS làm hỏng giao diện rồi commit: `"Wrong css: break layout and colors"` và push lên GitHub.
6. Sử dụng lệnh `git revert HEAD --no-edit` để hoàn tác commit hỏng mà không làm mất lịch sử các commit chuẩn trước đó. Sau khi revert xong, tiếp tục push commit revert lên GitHub để hoàn tất.

### 2. Kết quả lịch sử commit trên GitHub

Lệnh `git log --oneline` thể hiện rõ toàn bộ tiến trình làm việc:
```text
0fdfb33 Revert "Wrong css: break layout and colors"
43d250f Wrong css: break layout and colors
220af49 Style introduction section
c750598 Add introduction section
229728d Initial structure
```

### 3. Link GitHub repository Bài 6
- Đường link nộp bài: https://github.com/DK3XDK2/personal-portfolio
