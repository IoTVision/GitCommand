# Git

# Cấu trúc Git

Git bao gồm 3 thành phần cơ bản sau:

 * Local: Đây là nơi file có thể thay đổi, sửa xóa tùy ý như một file thông thường, không có bất cứ tác động nào của git nếu không được git theo dõi (tracking), nơi này nằm trong máy tính
 * Repository: Một khi file được thêm vào đây, nó sẽ được theo dõi (tracking) với local, bất cứ sự thay đổi nào giữa nội dung file thuộc repo và nội dung của chính file đó trên local đều được git so sánh sự khác nhau nội dung file. Nơi này nằm trong máy tính
 * Remote: đây là server git trên github, dùng để lưu trữ, đồng bộ file giữa các developer với nhau, sửa lỗi issue phát sinh, phát hành bản chính outsource code..., nơi này nằm trên cloud

# Thao tác cơ bản với git
## Chuẩn bị
- Đăng ký tài khoản github
- Tải [Git Bash](https://git-scm.com/downloads)
- Tạo một repository trống trên github
## Thao tác với git trên local
1. Chọn một thư mục Workspace, mở **Git Bash** tại đây và gõ:
```
git init
```
Lúc này một **Repository** trống sẽ xuất hiện và có tên nhánh mặc định là **master**

2. Tạo một file a.txt
```
touch a.txt
```
Thêm nội dung vào a.txt
```
Làm việc với git
```
3. Save lại và thoát, trên **Git Bash** gõ:
```
git add a.txt
```
File a.txt được thêm vào cached của **Repository**, lúc này file a.txt đang ở trạng thái **staged change**. 

Nếu có nhiều file muốn **add** cùng lúc thì:
```
git add .
```

4. Gõ:
```
git commit -m "Thêm file a.txt"
```
Khi gọi lệnh **commit**, **Repository** sẽ lưu lại nội dung của file a.txt, option __*-m*__ dùng để ghi lại nội dung commit dưới dạng **Tiêu đề** (ghi nội dung chính, vắn tắt những gì mình đã thay đổi, thêm, sửa, xóa ...), nếu không có option __*-m*__ thì commit sẽ được ghi chi tiết (sẽ nói chi tiết hơn ở lệnh commit)

5. Liên kết giữa local với remote:

```
git remote add origin <đường link dẫn tới remote>
```
* Thay thế <đường link dẫn tới remote> bằng tên của đường link thực tế tạo ở mục **Chuẩn bị**

6. Đẩy file lên remote:
```
git push 

fatal: The current branch master has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin master
```
Gõ lại theo lệnh được git gợi ý:
```
git push --set-upstream origin master
```
Vậy là đã hoàn thành việc đẩy dữ liệu lên git remote từ local

## Đồng bộ thông tin từ remote xuống local
Nếu Workspace trống chưa có git, thực hiện clone git từ remote
```
git clone <Link dẫn tới Repository>
```
Nếu Workspace đã liên kết với remote và đồng bộ nội dung mới các file:
```
git pull
```

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

### __*git rm --cached*__

Ngược với **git add** là **git rm --cached** dùng để bỏ theo dõi (tracking) các file

* Sử dụng option __*.*__ để add tất cả vào cùng lúc
* Sử dụng thêm option __*-r*__ nếu trong cache có folder

Example:

```
git rm --cached a.txt
rm 'a.txt'

git rm -r --cached .
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

__*Lưu ý*__:

Sau khi __*amend commit*__ nếu đẩy lên trên remote bằng lệnh **git push** thì sẽ gặp hiện tượng sau:

```
To https://github.com/Username/abc.git
 ! [rejected]        test -> test (non-fast-forward)
error: failed to push some refs to 'https://github.com/Username/abc.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```
Vì khi dùng __*amend*__, Git sẽ tạo ra một nhánh mới khác với nhánh đã thực hiện commit trước đó, nên trên remote sẽ thấy commit hiện tại trên local đang bị bỏ lại phía sau so với chính nó trên remote. Để khắc phục thì ta dùng lệnh **git push** với option __*f*__ để ép đẩy commit lên remote

```
git push -f
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

### __*git branch*__
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

### __*git checkout (hay git switch)*__

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

### __*git clone*__
Dowload __*Repository*__ từ Remote (server github) xuống local __*Repo*__

```
git clone <Đường link dẫn tới Repo đó>
```

### __*git remote*__

Đây là lệnh thao tác với Repository của **Remote** trên server github


option **add**: Liên kết **Local** với **Remote**, cho phép push dữ liệu từ Repository ở **Local** lên **Remote** và pull dữ liệu từ Remote về local
```
git remote add origin <Đường link remote>
```
__*Lưu ý*__: origin là bí danh (alias hay tên thay thế cho đường link remote để rút gọn lại tên gọi cho các lệnh sau này)

option **rm**: Hủy liên kết giữa **Local** và **Remote**

```
git remote rm origin
```

### __*git push*__

Đẩy commit từ local lên remote

__*Lưu ý*__: Nếu không set upstream branch thì sẽ báo lỗi sau: 



```
fatal: The current branch master has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin master
```

Có thể hiểu là nhánh hiện tại không nắm được thông tin của nhánh trên remote, nó không biết phải push lên nhánh nào, nếu nhánh hiện tại là **master** thì hãy dùng lệnh **git push --set-upstream origin master** để push lên remote nhánh master 

Còn nếu muốn push sang nhánh khác (không trùng tên với nhánh hiện tại) thì dùng lệnh sau: **git push -u origin <Tên nhánh>**

option __*f*__ : bắt buộc đẩy commit từ local lên remote, bỏ qua tất cả các điều kiện ràng buộc

```
git push -f 
```

option __*d*__ (hoặc __*delete*__): xóa nhánh trên remote

```
git push -d <Tên remote> <nhánh cần xóa>
git push -d origin dev
git push origin --delete <nhánh cần xóa>
```

**git push -u origin <Tên nhánh>**: dùng để push lên nhánh được đặt tên

### __*git log*__

In ra lịch sử commit chi tiết (ngày giờ, mail người commit, nội dung commit chi tiết)

```
git log
```

option **--oneline**: in vắn tắt tiêu đề commit và mã số commit

```
git log --oneline
```

option **--graph**: dùng để hiển thị commit theo dạng biểu đồ

```
git log --oneline --graph
```

### __*git status*__

Kiểm tra trạng thái hiện tại của **Repository**

### __*git restore*__

Khôi phục file về trạng thái trước đó

option **--stage**: Khôi phục lại những file ở trạng thái stage về trạng thái unstage (change) (trở lại trạng thái trước khi dùng git add)

Sử dụng option '.' để add tất cả vào cùng lúc

```
git restore --stage <file cần restore>
```

### __*git merge*__

Hợp nhất **Repository** của nhánh hiện tại với **Repository** của nhánh cần merge

```
git merge <nhánh cần merge>
```

option **--abort** dùng để hủy hợp nhất

```
git merge --abort
```
### __*git pull*__

Đồng bộ file giữa nhánh trên local và remote 

### __*git tag*__

* Gắn nhãn cho commit cũ:

```
git tag -a <Tag> <mã commit>
git tag -a V1.0.2 abcdef

```

* Hiển thị tất cả tag: 

```
git tag
```


* Push tag lên remote: git push origin <Tag>

* Đẩy hết tag lên git: 

```
git push origin --tags
```


* Xóa tag local: 

```
git tag -d <Tag>
git tag -d V1.0.2
```

### __*git submodule*__

git submodule add < remote_url >  < thư mục chứa submodule >

```
git submodule add https://github.com/Username/abc.git subfolder
```
Lúc này repo abc sẽ được chứa trong thư mục subfolder


# Git ignore 

Git ignore là một file dùng để loại những file/thư mục không mong muốn đưa vào **Repository** khi dùng **"git add ."**. Lý do có thể các file/ thư mục đó là file build được sinh ra khi chạy, thư mục chứa thư viện do phần mềm sinh code tạo ra, những nội dung có dung lượng lớn, khi upload/download server github sẽ bị chậm đi

Tạo ra một file **.gitignore** trên command line:

```
git init (nếu chưa khởi tạo repo)

touch .gitignore
```

__*Lưu ý*__ : những file/thư mục nào trước đó đã được stage change (dùng **git add**) thì khi được thêm vào **.gitignore**, file/thư mục đó vẫn không bị ignore vì chúng đã được **cached** bởi **Repository**, để khắc phục việc này, cần phải uncached bằng lệnh:

```
git rm -r --cached
``` 
Sau đó cached lại:
```
git add .
```
Có thể kiểm tra lại để xem các file được staged change bằng lệnh:
```
git status
```

## Cách sử dụng .gitignore

Giả sử có một folder cấu trúc như sau:
```
Project
|---Core/
|    |----Src/
|    |     |-- main.c
|    |     |-- filea.c
|    |     |-- fileb.c
|    |     |-- etc.c
|    |----Startup/
|
|---Inc/
|    |-- main.h
|    |-- filea.h
|    |-- fileb.h
|    |-- etc.h
|
|---Drivers/
|
|---Debug/
|config.txt
|config.h
|UserConfig.txt
|Temp.txt
|UserTemp.c
|UserTemp.h
```

1. Tạo **Repository**
```
git init
```
2. Tạo file **.gitignore**
```
touch .gitignore
```
3. Thêm nội dung vào .gitignore

```
# ignore thư mục Debug
Debug/
# ignore thư mục Drivers
Drivers/
# Giữ lại file main.c trong thư mục Core, phần còn lại ignore hết
Core/*
!Core/Src/main.c
# Giữ lại file main.h trong thư mục Inc, phần còn lại ignore hết
Inc/*
!Inc/main.h
# ignore thư mục Startup, giữ lại Src
Core/Startup/*
# ignore các file có đuôi .txt
*.txt
# ignore các file bắt đầu bằng User
User*
# ignore các file bắt đầu bằng User nhưng giữ lại đuôi .h
User*
!User*.h
```
# Hướng dẫn checkout branch ở remote với lần đầu clone repository về local 


1. Clone Repository về máy:

```
git clone <đường dẫn của repo>
```

2. Kiểm tra sau khi clone thì repository trên local đã có đầy đủ các nhánh chưa bằng git pull:

```
git pull
```
Nếu repository đã cập nhật đầy đủ thì command window sẽ trả về
```
Already up to date.
```
3. Checkout vào branch mình cần trên remote:
```
git checkout -- track origin/<branch cần checkout>
```
Kết quả thông báo việc checkout qua nhánh đã thành công 
```
Switched to a new branch '<branch cần checkout>'
branch '<branch cần checkout>' set up to track 'origin/<branch cần checkout>'
```
__*Lưu ý*__: Những lần checkout sau này sang các branch khác trên remote, chỉ cần sử dụng git checkout bình thường, không cần gõ thêm --track origin
```
git checkout <branch #2 cần checkout>
Switched to a new branch '<branch #2 cần checkout>'
branch '<branch #2 cần checkout>' set up to track 'origin/<branch #2 cần checkout>'
```