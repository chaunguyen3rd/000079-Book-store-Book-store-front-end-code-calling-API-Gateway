---
title : "Cài đặt và kích hoạt CORS"
date :  "`r Sys.Date()`" 
weight : 2
chapter : false
pre : " <b> 4.2 </b> "
---
Trong phần này chúng ta sẽ thêm cài đặt hỗ trợ binary file và kích hoạt CORS cho API.

1. Đi đến trang **API Settings**.
    - Nhấn vào **API Settings** ở menu bên trái.
    - Nhấn vào **Manage media types**.
![CreateRestAPI](/images/temp/1/65.png?width=90pc)

2. Ở trang **Manage binary media types**.
    - Nhấn nút **Add binary media type**.
    - Nhập **multipart/form-data**.
    - Nhấn nút **Save Changes**.
![CreateRestAPI](/images/temp/1/66.png?width=90pc)

3. Trở về trang **Resource**.
    - Nhấn nút **Resources**.
    - Chọn tài nguyên **/books**.
    - Chọn **Enable CORS**.
![CreateRestAPI](/images/temp/1/67.png?width=90pc)

4. Ở trang **Enable CORS**.
    - Chọn **GET** và **POST** ở **Access-Control-Allow-Methods**.
    - Giữ mọi thứ mặc định và bấm **Save**.
![CreateRestAPI](/images/temp/1/68.png?width=90pc)

5. Ở trang **Resources**.
    - Nhấn nút **Resources**.
    - Chọn tài nguyên **/{id}**.
    - Chọn **Enable CORS**.
![CreateRestAPI](/images/temp/1/69.png?width=90pc)

6. Ở trang **Enable CORS**.
    - Chọn **DELETE** ở **Access-Control-Allow-Methods**.
    - Giữ mọi thứ mặc định và bấm **Save**.
![CreateRestAPI](/images/temp/1/70.png?width=90pc)

7. Để front-end sử dụng được API, chúng ta cần triển khai API. Quay về trang **Resources**.
    - Nhấn vào **Resources**.
    - Chọn tài nguyên **/**.
    - Nhấn vào **Deploy API**.
![CreateRestAPI](/images/temp/1/71.png?width=90pc)

10. Ở hộp thoại **Deploy API**.
    - Chọn **New stage**.
  ![CreateRestAPI](/images/temp/1/72.png?width=90pc)
    - Nhập tên giai đoạn, ví dụ: **staging**.
    - Nhấn vào **Deploy**.
  ![CreateRestAPI](/images/temp/1/73.png?width=90pc)

12. Lưu địa chỉ URL lại để gọi API. Đi đến trang **Stages**.
    - Nhấn vào **Stages**.
  ![CreateRestAPI](/images/temp/1/74.png?width=90pc)
    - URL của **list** và **write** API:
  ![CreateRestAPI](/images/temp/1/75.png?width=90pc)
    - URL của **delete** API:
  ![CreateRestAPI](/images/temp/1/76.png?width=90pc)