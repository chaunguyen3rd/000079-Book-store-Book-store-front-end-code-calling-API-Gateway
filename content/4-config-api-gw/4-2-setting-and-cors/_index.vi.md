---
title : "Thiết lập và kích hoạt CORS"
date :  "`r Sys.Date()`" 
weight : 2
chapter : false
pre : " <b> 4.2 </b> "
---

Trong phần này, chúng ta sẽ thêm cài đặt hỗ trợ tệp nhị phân và kích hoạt CORS cho các API.

1. Đi đến trang **API Settings**.
    - Nhấp vào **API Settings** ở menu bên trái.
    - Nhấp vào **Manage media types**.
      ![CreateRestAPI](/images/temp/1/65.png?width=90pc)

2. Tại trang **Manage binary media types**.
    - Nhấp vào **Add binary media type**.
    - Nhập `multipart/form-data`.
    - Nhấp vào **Save Changes**.
      ![CreateRestAPI](/images/temp/1/66.png?width=90pc)

3. Quay lại trang **Resource**.
    - Nhấp vào **Resources**.
    - Chọn resource **/books**.
    - Chọn **Enable CORS**.
      ![CreateRestAPI](/images/temp/1/67.png?width=90pc)

4. Tại trang **Enable CORS**.
    - Chọn **GET** và **POST** cho mục **Access-Control-Allow-Methods**.
    - Để mặc định và nhấp vào **Save**.
      ![CreateRestAPI](/images/temp/1/68.png?width=90pc)

5. Tại trang **Resources**.
    - Nhấp vào **Resources**.
    - Chọn resource **/{id}**.
    - Chọn **Enable CORS**.
      ![CreateRestAPI](/images/temp/1/69.png?width=90pc)

6. Tại trang **Enable CORS**.
    - Chọn **DELETE** cho mục **Access-Control-Allow-Methods**.
    - Để mặc định và nhấp vào **Save**.
      ![CreateRestAPI](/images/temp/1/70.png?width=90pc)

7. Để front-end có thể sử dụng các API, chúng ta cần triển khai các API. Quay lại trang **Resources**.
    - Nhấp vào **Resources**.
    - Chọn resource **/**.
    - Nhấp vào **Deploy API**.
      ![CreateRestAPI](/images/temp/1/71.png?width=90pc)

8. Tại modal **Deploy API**.
    - Chọn **New stage**.
      ![CreateRestAPI](/images/temp/1/72.png?width=90pc)
    - Nhập tên stage, ví dụ: `staging`.
    - Nhấp vào **Deploy**.
      ![CreateRestAPI](/images/temp/1/73.png?width=90pc)

9. Ghi chú URL để gọi API. Đi đến trang **Stages**.
    - Nhấp vào **Stages**.
      ![CreateRestAPI](/images/temp/1/74.png?width=90pc)
    - URL của API **list** và **write**:
      ![CreateRestAPI](/images/temp/1/75.png?width=90pc)
    - URL của API **delete**:
      ![CreateRestAPI](/images/temp/1/76.png?width=90pc)
