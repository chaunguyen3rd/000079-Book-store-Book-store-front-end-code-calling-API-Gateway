---
title : "Cài đặt và kích hoạt CORS"
date :  "`r Sys.Date()`" 
weight : 2
chapter : false
pre : " <b> 4.2 </b> "
---
Trong phần này chúng ta sẽ thêm cài đặt hỗ trợ binary file và kích hoạt CORS cho API
1. Chọn **API Settings** ở menu phía bên trái
    - Ấn vào ***Manage media types**
![CreateRestAPI](/images/1/55.png?width=90pc)

2. Click **Add binary media type**
    - Nhập **multipart/form-data**
    - Ấn nút **Save Changes**
![CreateRestAPI](/images/1/56.png?width=90pc)

3. Sau khi cài đặt xong, quay lại **Resource** ở menu bên trái.
    - Chọn **/books** resource
    - Chọn **Enable CORS**
![CreateRestAPI](/images/1/57.png?width=90pc)

4. Tại phần **Enable CORS**
    - Chọn phương thức **GET** and **POST** 
    - Click **Save**
![CreateRestAPI](/images/1/58.png?width=90pc)

6. Chọn **/{id}** resource
    - Chọn **Enable CORS**
![CreateRestAPI](/images/1/59.png?width=90pc)

7. Tại mục **Enable CORS**
    - Chọn phương thức **DELETE** 
    - Click **Save**
![CreateRestAPI](/images/1/60.png?width=90pc)

9. Để front-end có thể sử dụng API, chúng ta cần deploy chúng.
    - Chọn **/** resource
    - Nhấn **Deploy API**
![CreateRestAPI](/images/1/61.png?width=90pc)

10. Chọn **New stage**
![CreateRestAPI](/images/1/62.png?width=90pc)
11. Nhập tên cho stage, ví dụ: **staging**
    - Click **Deploy**
![CreateRestAPI](/images/1/63.png?width=90pc)

12. Ghi lại URL để gọi API
![CreateRestAPI](/images/1/64.png?width=90pc)


    - URL của API đọc và ghi:
![CreateRestAPI](/images/1/65.png?width=90pc)

    - URL của API xoá:
![CreateRestAPI](/images/1/67.png?width=90pc)