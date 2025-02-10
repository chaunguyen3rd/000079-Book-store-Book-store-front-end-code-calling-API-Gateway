---
title : "Viết hàm Lambda"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 3.2.1 </b> "
---
Trong bước này, chúng ta sẽ cập nhật mã cho hàm **book_create** đã tạo ở bài 1.

1. Mở [AWS Lambda console](https://us-east-1.console.aws.amazon.com/lambda/home?region=us-east-1#/functions).
    - Nhấp vào **Functions** ở menu bên trái.
    - Chọn hàm **book_create**.
      ![LambdaConsole](/images/temp/1/23.png?width=90pc)

2. Tải tệp mã nguồn về thiết bị của bạn.
{{%attachments title="Source code" pattern=".*\.(zip)$"/%}}

3. Tại trang **book_create**.
    - Nhấp vào nút **Upload from**.
    - Chọn **.zip file**.
      ![LambdaConsole](/images/temp/1/24.png?width=90pc)

4. Tại modal **Upload a .zip file**.
    - Nhấp vào nút **Upload** và chọn tệp mã nguồn đã tải xuống.
    - Nhấp vào **Save**.
      ![LambdaConsole](/images/temp/1/25.png?width=90pc)

5. Tại trang **book_create**.
    - Nhấp vào tab **Configuration**.
    - Nhấp vào **Environment variables** ở menu bên trái.
    - Nhấp vào **Edit**.
      ![CreateFunction](/images/temp/1/26.png?width=90pc)

6. Tại trang **Edit environment variables**.
    - Nhấp vào **Add environment variable**, sau đó thêm các biến môi trường sau:
      - `BUCKET_NAME`: Nhập tên bucket, ví dụ `book-image-stores-by-myself`.
      - `BUCKET_RESIZE_NAME`: Nhập tên bucket, ví dụ `book-image-resize-stores-by-myself`.
      - `TABLE_NAME`: Nhập tên bảng, ví dụ `Books`.
    - Sau đó nhấp vào **Save**.
      ![CreateFunction](/images/temp/1/27.png?width=90pc)

7. Cấp quyền cho hàm Lambda để ghi tệp vào bucket S3.
    - Nhấp vào tab **Configuration**.
    - Chọn mục **Permissions** ở menu bên trái.
    - Nhấp vào vai trò mà hàm đang thực thi.
      ![CreateFunction](/images/temp/1/28.png?width=90pc)

8. Tại trang **book_create-role-...**.
    - Nhấp vào chính sách hiện có bắt đầu bằng **AWSLambdaExecutionRole-...**.
      ![CreateFunction](/images/temp/1/29.png?width=90pc)

9. Tại trang **AWSLambdaBasicExecutionRole-...**.
    - Nhấp vào **Edit**.
      ![CreateFunction](/images/temp/1/30.png?width=90pc)

10. Tại trang **Step 1: Modify permissions in AWSLambdaBasicExecutionRole-**.
    - Thêm khối json dưới đây vào **Policy editor**.

      ```json
      {
                  "Effect": "Allow",
                  "Action": "s3:PutObject",
                  "Resource": "arn:aws:s3:::book-image-stores-by-myself/*"
              }
      ```

    - Nhấp vào **Next**.
      ![CreateFunction](/images/temp/1/31.png?width=90pc)

11. Tại trang **Step 2: Review and save**.
    - Xem lại các thiết lập và nhấp vào **Save changes**.
      ![CreateFunction](/images/temp/1/32.png?width=90pc)
