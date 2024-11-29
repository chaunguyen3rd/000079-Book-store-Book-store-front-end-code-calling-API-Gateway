---
title : "Tạo các method"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 4.1 </b> "
---
#### Tạo API đọc
1. Ấn nút **/books**, sau đó chọn **Create method**
![CreateListAPI](/images/1/44.png?width=90pc)
2. Tại mục **Method detail** 
    - Chọn method **GET**
    - Chọn **Lambda Function** cho **Integration type**
    - Tích vào mục **Use Lambda Proxy integration**
    - Nhập tên của Lambda function cần tích hợp: **books_list**
    - Ấn nút **Save**
![CreateListAPI](/images/1/45.png?width=90pc)

3. Click **Create method**
![CreateListAPI](/images/1/46.png?width=90pc)

#### Tạo API ghi
1. Ấn nút **/books**, sau đó chọn **Create method**
![CreateListAPI](/images/1/47.png?width=90pc)

2. Tại mục **Method detail** 
    - Chọn method **POST**
    - Chọn **Lambda Function** cho **Integration type**
    - Tích vào mục **Use Lambda Proxy integration**
    - Nhập tên của Lambda function cần tích hợp: **books_list**
    - Ấn nút **Save**
![CreateListAPI](/images/1/48.png?width=90pc)

3. Click **Create method**
![CreateListAPI](/images/1/49.png?width=90pc)

#### Tạo API xoá

1. Ấn nút **/books**, sau đó chọn **Create Resource**
![CreateListAPI](/images/1/50.png?width=90pc)

2. Tại phần **Create Resource**
    - Nhập **{id}** cho mục **Resource name**
    - Ấn nút **Create Resource**
![CreateListAPI](/images/1/51.png?width=90pc)
3. Nhấn vào **/{id}**, sau đó chọn **Create method**
![CreateListAPI](/images/1/52.png?width=90pc)
4. **Tại mục Method detail**
    - Chọn method **DELETE**
    - Chọn **Lambda Function** cho **Integration type**
    - Tích vào mục **Use Lambda Proxy integration**
    - Nhập tên của Lambda function cần tích hợp: **book_delete**
    - Ấn nút **Save**
![CreateListAPI](/images/1/53.png?width=90pc)
5. Nhấn vào **Create method**
![CreateListAPI](/images/1/54.png?width=90pc)
Vậy là chúng ta đã tạo xong các API tương tác với Lambda function.