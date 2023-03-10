# GitCommand

# Cấu trúc Git

Git bao gồm 3 thành phần cơ bản sau:

 * Local: Đây là nơi file có thể thay đổi, sửa xóa tùy ý như một file thông thường, không có bất cứ tác động nào của git nếu không được git theo dõi (tracking)
 * Repository: Một khi file được thêm vào đây, nó sẽ được theo dõi (tracking) với local, bất cứ sự thay đổi nào giữa nội dung file thuộc repo và nội dung của chính file đó trên local đều được git so sánh sự khác nhau nội dung file.
 * Remote: đây là server git trên github, dùng để lưu trữ, đồng bộ file giữa các developer với nhau, sửa lỗi issue phát sinh, phát hành bản chính outsource code...
 
# Các lệnh thường dùng

### __*git init*__ 
Khởi tạo một git repository ( folder .git/)

Ví dụ
```
git init
Initialized empty Git repository in C:/abc/.git/
```

### __*git add*__ 
Thêm file vào **Repository** để thực hiện **tracking**

Ví dụ:
```
git add a.txt b.txt c.txt d.txt
```

* Sử dụng option '.' để add tất cả vào cùng lúc

```
git add .
```

### __*git commit*__ 
Lưu tiến trình tiếp theo của file được **Repository** tracking (giống như save game trong quá trình chơi) so với commit trước đó (thêm, sửa xóa gì so với commit trước đó của file)

* Option __*-m*__ dùng để ghi lại tiêu đề nội dung cần commit

```
git commit -m "This is first commit"
```

* Option __*--amend*__ dùng để vá lại commit bị lỗi (do thiếu thông tin, thay đổi nội dung commit...)

```
git commit --amend -m "Amend commit above because it is wrong"
```

* Nếu không có option __*-m*__ thì nội dung commit sẽ được ghi chi tiết hơn (bao gồm cả ghi tiêu đề commit và nội dung chi tiết về từng thay đổi so với commit trước đó), lúc này git sẽ mở một text editor (vim hoặc nano) để chỉnh sửa chi tiết

    * Dòng đầu tiên là tiêu đề của commit
    
    * Dòng thứ 2 cần bỏ trống để phân biệt tiêu đề và nội dung chi tiết
    
    * Dòng 3 trở xuống dùng để ghi nội dung chi tiết commit

Ví dụ:
1. Gõ lệnh sau:

```
git commit 
```
2. Git sẽ mở ra một text editor như sau:
    * Lúc này ta cần gõ phím I trên bàn phím để vào chế độ INSERT (ghi nội dung file), cuối dòng sẽ hiện ra chữ INSERT để thông báo đã vào chế độ INSERT
    
```
Đây là dòng tiêu đề

Đây là nội dung chi tiết commit
File a.txt đã thay đổi ...
File b.txt đã thay đổi ...
File c.txt đã thay đổi ...
File c.txt đã thay đổi ...

```
3. Sau khi ghi xong, nhấn Ctrl+C để thoát INSERT, gõ  __*:wq*__ (Write and Quit) để save và thoát commit

### git branch
Tạo ra một nhánh mới từ mã số commit đang dùng của nhánh hiện tại (lưu ý nếu không có commit nào thì không dùng được)
```
git branch SpiritBoi
```
Tạo ra nhánh tên SpiritBoi từ mã commit hiện tại

Để xóa nhánh ta thêm option __*-d*__ như sau:
```
git branch -d SpiritBoi
```
Để kiểm tra tất cả các nhánh hiện có thì dùng git branch với không có tên và option theo sau:

```
git branch
```

### git checkout

- Với option __*b*__: Tạo ra một nhánh mới từ mã số commit đang dùng của nhánh hiện tại và nhảy tới nhánh đó

```
git checkout -b SpiritBoi
```

Kết quả:

```
Switched to a new branch 'SpiritBoi'
```

- Không có option __*b*__ : nhảy sang nhánh đã tồn tại
 
```
git checkout SpiritBoi
```

- git checkout --track origin/<Tên nhánh trên remote>

Tạo một nhánh local có tên trùng với tên nhánh trên remote, tải thông tin từ nhánh remote sang nhánh local (ví dụ Develop) và nhảy sang nhánh local

Ví dụ

```
git checkout --track origin/Develop
```

### git clone
Dowload __*Repository*__ từ Remote (server github) xuống local __*Repo*__

```
git clone <Đường link dẫn tới Repo đó>
```

### git remote add origin
Liên kết local với remote, cho phép push dữ liệu từ Repo local lên Remote
```
git remote add origin <Dường link remote>
```
__*Lưu ý*__: origin là bí danh (alias hay tên thay thế cho đường link remote để rút gọn lại tên gọi cho các lệnh sau này)

### git push: 
đẩy commit từ local lên remote
