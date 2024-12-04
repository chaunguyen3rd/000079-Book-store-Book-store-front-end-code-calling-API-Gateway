---
title : "Tạo các method"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 4.1 </b> "
---
#### Tạo API đọc
1. Ở trang **Resource**.
    - Nhấn vào **/books**, sau đó chọn **Create method**.
![CreateRestAPI](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/55.png?width=90pc)

2. Ở trang **Create method**.
    - Chọn phương thức **GET**.
    - Chọn **Lambda function** ở **Integration type**.
    - Bật **Lambda proxy integration**.
    - Nhập tên lambda function được liên kết: **books_list**.
  ![CreateRestAPI](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/56.png?width=90pc)
    - Kéo xuống dưới cùng và bấm vào **Create method**.
  ![CreateRestAPI](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/57.png?width=90pc)

#### Tạo API ghi
1. Ở trang **Resource**.
    - Bấm vào **/books**, sau đó chọn **Create method**.
![CreateRestAPI](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/55.png?width=90pc)

2. Ở trang **Create method**.
    - Chọn giao thức **POST**.
    - Chọn **Lambda function** ở **Integration type**.
    - Bật **Lambda proxy integration**.
    - Nhập tên lambda function được liên kết: **book_create**.
  ![CreateRestAPI](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/58.png?width=90pc)
    - Kéo xuống dưới cùng và bấm vào **Create method**.
  ![CreateRestAPI](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/59.png?width=90pc)

#### Tạo API xoá
1. Ở trang **Resource**.
    - Nhấn **/books**, sau đó nhấn vào **Create resource**.
![CreateRestAPI](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/60.png?width=90pc)

2. Ở trang **Create resource**.
    - Nhập **{id}** for **Resource name**.
    - Nhấn vào **Create Resource**.
![CreateRestAPI](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/61.png?width=90pc)

3. Ở trang **Resource**.
    - Nhấn vào **/{id}**.
    - Chọn **Create method**.
![CreateRestAPI](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/62.png?width=90pc)

4. Ở trang **Create method**.
    - Chọn giao thức **DELETE**.
    - Chọn **Lambda function** ở **Integration type**.
    - Bật **Lambda proxy integration**.
    - Nhập tên lambda function được liên kết: **book_delete**.
  ![CreateRestAPI](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/63.png?width=90pc)
    - Kéo xuống dưới cùng và bấm vào **Create method**.
  ![CreateRestAPI](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/64.png?width=90pc)

Vậy là chúng ta đã tạo xong các API tương tác với Lambda function.