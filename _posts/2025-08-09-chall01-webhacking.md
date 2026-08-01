---
title: web-hacking.kr | Chall01
date: 2025-08-09
tags: [ctf, webhacking.kr]
categories: [Writeups, CTF]
author: bumbi.203_
---

# Chall01 

* Giao diện web
![image](/assets/img/CTF/webhacking.kr/chall01/image1.png)

Sau khi view source thì như sau: 

![image](/assets/img/CTF/webhacking.kr/chall01/image2.png)

* Khai thác 

Chú ý phần code PHP có logic được giải thích như sau: 
- Nếu cookie được gán vào trường `user_lv` và kiểm tra ko phải là số thì gán bằng **1** 
- Nếu cookie >= 4 thì gán bằng **1**
- Nếu cookie > 3 thì `solve`. 

Nên mình chèn bằng `3.1` thì thỏa mãn code PHP này. 

![image](/assets/img/CTF/webhacking.kr/chall01/image3.png)




