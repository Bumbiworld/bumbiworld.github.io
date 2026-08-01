---
title: Recon GitHub - RT
date: 2025-10-09
tags: [recon, redteam]
categories: [Writeups, RT]
author: bumbi.203_
---

# Recon Github

> Mục tiêu 1: tìm đến đường dẫn một trang blog cũ của **`CJ23Group`**
> 

### Google

---

Đầu tiên ta thực hiện search google về từ khóa **`CJ23Group`** + **`github`** 

![image.png](/assets/img/redteam/Recon/github/image.png)

Mình vào thử trong trang xem thử có gì ?

![image.png](/assets/img/redteam/Recon/github/image1.png)

Tại đây thì mình chỉ thấy có một chức năng **`CONTACT US`** 

![image.png](/assets/img/redteam/Recon/github/image2.png)

### Github Search

---

Có vẻ là không có thông tin gì → nên mình dùng **`Github Search`** 

![image.png](/assets/img/redteam/Recon/github/image3.png)

Mình tìm ra repo có liên quan 😎 → nhảy vào xem thử

![image.png](/assets/img/redteam/Recon/github/image4.png)

Có vẻ đây đúng là repo dành cho web blog trên. 

Khi tìm ra github thì mình nên vào đọc commit.

![image.png](/assets/img/redteam/Recon/github/image5.png)

Đọc qua các commit thì mình tìm dược đoạn như sau: 

![image.png](/assets/img/redteam/Recon/github/image6.png)

Thì đây có vẻ đường link cũ của blog này 

![image.png](/assets/img/redteam/Recon/github/image7.png)

**`CBJS{http://blog.cj23group.com/innovation-projects-and-blog/}`**

> Mục tiêu 2: Tìm Github cá nhân của nhân viên thuộc tổ chức **`CJ23Group`**
> 

Thì trong commit lúc thì quan sát xem ai đã commit 

![image.png](/assets/img/redteam/Recon/github/image8.png)

Đó là **`ak4txuk1`** → cho nên mình tìm về profile user này trên github **`https://github.com/ak4txuk1`**

![image.png](/assets/img/redteam/Recon/github/image9.png)

**`CBJS{https://github.com/ak4txuk1}`**

> Mục tiêu 3: tìm username/password trong repo của nhân viên
> 

Từ profile này thì mình thấy có một repo 😎

Mình tiến hành search trong repo này thôi 😀 

![image.png](/assets/img/redteam/Recon/github/image10.png)

> Mục tiêu 4:  Xác định thời gian anh nhân viên ở Lab 1.2 đã bất cẩn commit credential lên repo **`php-todo-list`**.
> 

Giờ mình xác định thời gian đã commit credential lên github. 

Nó nằm trong **`todo.class.php`** 

![image.png](/assets/img/redteam/Recon/github/image11.png)

Nhưng sau khi đi vào phần commit thì quá nhiều commit 😣 Cho nên mình sẽ dùng 1 tool 😎 → **`gitleaks`** 

![image.png](/assets/img/redteam/Recon/github/image12.png)

Sau đó mình đọc **`report.json`** 

Mình phát hiện ra khá nhiều thứ thú vị 😎 

![image.png](/assets/img/redteam/Recon/github/image13.png)

`CBJS{2023-09-14}`
