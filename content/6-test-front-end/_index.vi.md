---
title : "Kiểm tra API với front-end"
date :  "`r Sys.Date()`" 
weight : 6
chapter : false
pre : " <b> 6. </b> "
---
Sau khi kiểm tra các API hoạt động đúng với Postman, chúng ta sẽ kiểm tra các API được gọi với front-end xây dựng từ bước 2.

1. Mở tệp **config.js** trong thư mục **fcj-serverless-frontend** đã được tải về từ phần 2.
    - Thay giá trị cho **APP_API_URL** bằng URL của bạn.
![CreateRestAPI](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/83.png?width=90pc)
![CreateRestAPI](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/84.png?width=90pc)

2. Mở tệp **App.js** trong thư mục **fcj-serverless-frontend/src/**, sửa giá trị của biến **isAdmin** thành **true**.
![CreateRestAPI](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/85.png?width=90pc)

3. Chạy các dòng lệnh dưới đây.
    ```
    yarn build
    aws s3 cp build s3://fcj-book-store --recursive
    ```

4. Dán endpoint của S3 static web vào browser của bạn. Ứng dụng đã hiện thông tin sách, nhưng vẫn chưa có ảnh vì chúng ta chưa tải ảnh lên.
![CreateRestAPI](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/86.png?width=90pc)
Vậy API đọc dữ liệu đã hoạt động đúng.

5. Kiểm tra API ghi dữ liệu.
    - Ấn sang tab **Management**.
    - Ấn nút **Update**.
  ![CreateRestAPI](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/87.png?width=90pc)
    - Sửa bất kỳ thông tin gì bạn muốn trừ **id**.
    - Ấn nút **Choose image**.
    - Đưa ảnh dưới đây tải lên bucket:
    {{%attachments title="Image" pattern=".*\.(jpeg)$"/%}}
    - Ấn nút **Update**.
    - Ấn nút **OK**.
  ![CreateRestAPI](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/88.png?width=90pc)
    - Ảnh và thông tin được cập nhật
  ![CreateRestAPI](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/89.png?width=90pc)
    - Ấn sang tab **Create new book** ghi dữ liệu mới vào cơ sở dữ liệu.
    - Nhập id bằng **5**
    - Nhập tên: **Amazon Web Services in Action**
    - Nhập tác giả: **Andreas Wittig**
    - Nhập thể loại: **IT**
    - Nhập giá: **59.99**
    - Nhập mô tả: **Amazon Web Services in Action, Second Edition is a comprehensive introduction to computing, storing, and networking in the AWS cloud. You'll find clear, relevant coverage of all the essential AWS services you to know, emphasizing best practices for security, high availability and scalability.**

    {{%attachments title="Image" pattern=".*\.(jpg)$"/%}}

    - Ấn nút **Choose File** để tải ảnh lên.
    - Ấn nút **Create**.
    - Ấn nút **OK**.
  ![CreateRestAPI](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/90.png?width=90pc)
    - Hiển thị thông tin vừa tạo.
  ![CreateRestAPI](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/91.png?width=90pc)

6. Kiểm tra API xoá.  
    - Ấn sang tab **Management**.
    - Ấn nút **Update**.
  ![CreateRestAPI](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/92.png?width=90pc)
    - Ấn nút **Delete**.
    - Ấn nút **OK** để xác nhận xoá.
  ![CreateRestAPI](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/93.png?width=90pc)
    - Xem kết quả sau khi xoá: không còn xuất hiện thông tin sách nữa.
  ![CreateRestAPI](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/94.png?width=90pc)

Chúng ta đã hoàn thành việc xây dựng một ứng dụng web đơn giản theo mô hình serverless. 
