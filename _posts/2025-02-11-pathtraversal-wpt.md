---
title: Path Traversal - WPT
date: 2025-02-11
tags: [path traversal]
categories: [Writeups, wpt]
author: bumbi.203_
---
## 🧪 Level 1

---

![image](/assets/img/WPT/path-traversal/image1.png)

Mình thấy có nhiều hình ảnh. Nên sẽ thực hiện **`View`** thử.

![image](/assets/img/WPT/path-traversal/image2.png)

Quan sát thì thấy nó nhận vào tên ảnh vào biến **`file_name`** 

Mình tiến hành review source code. 

![image](/assets/img/WPT/path-traversal/image3.png)

Như vậy **`file_name`** nhận vào tên ảnh mà ảnh đang được đặt trong **`/var/www/html/img/`** nên mình truyền **`../../../../`** để có thể thoát ra ngoài.

![image](/assets/img/WPT/path-traversal/image4.png)

## 🧪 Level 2

---

Tương tự như giao diện ở level 1. 

Cho nên mình cũng ấn vào view thử hình ảnh. 

![image](/assets/img/WPT/path-traversal/image5.png)

Nó nhận vào **`img/flag.png`** qua tham số **`file`** 

Tiến hành review source code. 

![image](/assets/img/WPT/path-traversal/image6.png)

Quan sát thì mình đã bị chặn `..` , nhưng cách này vẫn chưa đủ chắc. 

Và hiện tại thì mình đang được đặt bên trong 1 folder nữa là **`img`** 

Nếu mình đã bị chặn thì sẽ truyền đường dẫn tuyệt đối.

![image](/assets/img/WPT/path-traversal/image7.png)

## 🧪 Level 3

---

![image](/assets/img/WPT/path-traversal/image8.png)

Mình được cho phép tạo một album và upload file vào album đó. 

Và khi mình ấn vào Download các file thì nó sẽ render ra hình ảnh.

![image](/assets/img/WPT/path-traversal/image9.png)

Tiến hành review source code.

![image](/assets/img/WPT/path-traversal/image10.png)

Quan sát thì mình nhìn thấy nó tạo ra thêm 1 folder bên trong **`/var/www/html/upload/<session>`** và folder album lại được nối chuỗi vào.

Nghĩa là khi mình tạo ra 1 album thì lúc đó đường dẫn sẽ là **`/var/www/html/upload/<session>/album`** 

Quan trọng hơn là mình cần đọc config của server hiện tại đang cho phép gì. 

![image](/assets/img/WPT/path-traversal/image11.png)

Tại đây quan sát thì mình đã bị tắt không cho phép **`.htaccess`** và tại dòng 44 là **`SetHandler None`** là không cho phép thực thi trong folder upload

Như vậy do nó nối folder upload vào trong tên **`album`** nên mình vẫn có thể **path traversal** để upload ra ngoài folder đó và thực thi được code.

![image](/assets/img/WPT/path-traversal/image12.png)

Sau đó mình truy cập vào file đã upload. 

![image](/assets/img/WPT/path-traversal/image13.png)

## 🧪 Level 4

---

![image](/assets/img/WPT/path-traversal/image14.png)

Đầu tiên mình cần nhập một username vào. 

![image](/assets/img/WPT/path-traversal/image15.png)

Tại **`Profile`** mình có chức năng **`Upload`** 

![image](/assets/img/WPT/path-traversal/image16.png)

Và tại phần **`Game`** 

![image](/assets/img/WPT/path-traversal/image17.png)

Mình tiến hành đọc source code.

Tại file **`register.php`** , quan sát thấy biến **`name`** nhưng được filter khá chặt và nó cũng ko rơi vào cái gì nguy hiểm nên mình tiếp tục xem xét.

![image](/assets/img/WPT/path-traversal/image18.png)

Còn file **`profile.php`** 

![image](/assets/img/WPT/path-traversal/image19.png)

Nó nối chuỗi vào **`/var/www/html/upload/<session>/avatar.jpg`** 

Nghĩa là giờ mình upload file gì thì nó cũng sẽ là **`avatar.jpg`** 

![image](/assets/img/WPT/path-traversal/image20.png)

Mình quan sát tiếp file **`game.php`** 

![image](/assets/img/WPT/path-traversal/image21.png)

Quan sát thì mình đang ở **`views/`** 

Cho nên mình cần truyền payload như sau:

![image](/assets/img/WPT/path-traversal/image22.png)

## 🧪 Level 5

![image](/assets/img/WPT/path-traversal/image23.png)

---

![image](/assets/img/WPT/path-traversal/image24.png)

Tại đây mình có game và nó nhận file vào bằng biến **`game`** 

Mình tiến hành review source code. 

![image](/assets/img/WPT/path-traversal/image25.png)

Tại đây nó dùng các hàm **`include`** để khi load trang thì nó sẽ load và thực thi các file đó. Nhưng tại dòng **`21`** thì nó đã nối biến **`$game`** vào **`./views/`** 

Như vậy thì mình thử truyền payload path treversal.

![image](/assets/img/WPT/path-traversal/image26.png)

Nhưng làm sao để RCE thì trên server sẽ có nơi ghi lại log. Nên mình sẽ quan sát file này. 

![image](/assets/img/WPT/path-traversal/image27.png)

Và nhìn thấy nó viết lại mọi thứ kể cả **`User-Agent`** , mình thử truyền shell vào trường này.

![image](/assets/img/WPT/path-traversal/image28.png)

## 🧪 Level 6

---

![image](/assets/img/WPT/path-traversal/image29.png)

Ở level này ta được upload 1 file **`zip` .** Tiến hành đọc source code.

![image](/assets/img/WPT/path-traversal/image30.png)

Như vậy nó sẽ kiểm tra nếu file là **`.zip`** thì nó sẽ **`unzip`** 

Khi mình đọc file config thì ta cũng không thể upload file **`.htaccess`** 

Sau khi mày mò thì mình vẫn ko thể tìm cách upload ra ngoài **`/var/www/html`** 

![image](/assets/img/WPT/path-traversal/image31.png)

Ở đây mình thấy tại dòng **`44`** nó kiểm tra là directory thì nó sẽ bỏ qua, và sau đó lấy khi content của file zip. Và sau đó rơi vào hàm **`file_put_contents`** 

Như vậy nếu mình tạo ra một file zip có payload là **`../../info.php`** và file **`info.php`** chứa payload thực thi. 

Điều này mình cần đến tool **`evilrca`** như sau: 

![image](/assets/img/WPT/path-traversal/image32.png)

Sau đó mình upload file này lên.

![image](/assets/img/WPT/path-traversal/image33.png)

Sau đó mình truy cập tới đường dẫn mình dùng payload.

![image](/assets/img/WPT/path-traversal/image34.png)