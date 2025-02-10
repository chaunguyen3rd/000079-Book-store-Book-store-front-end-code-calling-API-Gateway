---
title : "Tạo phương thức"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 4.1 </b> "
---
#### Tạo API liệt kê

1. Tại trang **Resource**.
    - Nhấp vào **/books**, sau đó chọn **Create method**.
      ![CreateRestAPI](/images/temp/1/55.png?width=90pc)

2. Tại trang **Create method**.
    - Chọn phương thức **GET**.
    - Chọn **Lambda function** cho mục **Integration type**.
    - Bật **Lambda proxy integration**.
    - Nhập tên hàm Lambda để tích hợp: `books_list`.
      ![CreateRestAPI](/images/temp/1/56.png?width=90pc)
    - Cuộn xuống dưới cùng và nhấp vào **Create method**.
      ![CreateRestAPI](/images/temp/1/57.png?width=90pc)

#### Tạo API ghi

1. Tại trang **Resource**.
    - Nhấp vào **/books**, sau đó chọn **Create method**.
      ![CreateRestAPI](/images/temp/1/55.png?width=90pc)

2. Tại trang **Create method**.
    - Chọn phương thức **POST**.
    - Chọn **Lambda function** cho mục **Integration type**.
    - Bật **Lambda proxy integration**.
    - Nhập tên hàm Lambda để tích hợp: `book_create`.
      ![CreateRestAPI](/images/temp/1/58.png?width=90pc)
    - Cuộn xuống dưới cùng và nhấp vào **Create method**.
      ![CreateRestAPI](/images/temp/1/59.png?width=90pc)

#### Tạo API xóa

1. Tại trang **Resource**.
    - Nhấp vào **/books**, sau đó nhấp vào **Create resource**.
      ![CreateRestAPI](/images/temp/1/60.png?width=90pc)

2. Tại trang **Create resource**.
    - Nhập `{id}` cho mục **Resource name**.
    - Nhấp vào **Create Resource**.
      ![CreateRestAPI](/images/temp/1/61.png?width=90pc)

3. Tại trang **Resource**.
    - Nhấp vào **/{id}**.
    - Chọn **Create method**.
      ![CreateRestAPI](/images/temp/1/62.png?width=90pc)

4. Tại trang **Create method**.
    - Chọn phương thức **DELETE**.
    - Chọn **Lambda function** cho mục **Integration type**.
    - Bật **Lambda proxy integration**.
    - Nhập tên hàm Lambda để tích hợp: `book_delete`.
      ![CreateRestAPI](/images/temp/1/63.png?width=90pc)
    - Cuộn xuống dưới cùng và nhấp vào **Create method**.
      ![CreateRestAPI](/images/temp/1/64.png?width=90pc)

Vậy là chúng ta đã tạo các API để tương tác với các hàm Lambda.
