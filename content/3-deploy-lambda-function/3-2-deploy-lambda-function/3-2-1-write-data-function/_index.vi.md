---
title : "Lambda function ghi dữ liệu"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 3.2.1 </b> "
---
Trong bước này chúng ta sẽ cập nhật lại code cho function **book_create** đã tạo ở bài số 1:

1. Mở bảng điều khiển của [AWS Lambda](https://ap-southeast-2.console.aws.amazon.com/lambda/home?region=ap-southeast-2#/functions).
    - Click **Functions**.
    - Choose **book_create** function.
![LambdaConsole](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/23.png?width=90pc)

2. Tải tệp mã nguồn code vào máy của bạn.
{{%attachments title="Source code" pattern=".*\.(zip)$"/%}}

3. Ở trang **book_create**.
    - Nhấn nút **Upload from**.
    - Chọn **.zip file**.
![LambdaConsole](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/24.png?width=90pc)

4. Ở hộp thoại **Upload a .zip file**.
    - Nhấn nút **Upload** và chọn tệp mã nguồn đã được tải về.
    - Nhấn nút **Save**.
![LambdaConsole](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/25.png?width=90pc)

5. Ở trang **book_create**.
    - Nhấn vào tab **Configuration**.
    - Nhấn vào **Environment variables** ở menu bên trái.
    - Nhấn vào **Edit**.
![CreateFunction](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/26.png?width=90pc)

6. Ở trang **Edit environment variables**.
    - Nhấn **Add environment variable**, sau đó thêm những biến môi trường sau:
      - **BUCKET_NAME**: Nhập tên bucket, ví dụ **book-image-stores-by-myself**.
      - **BUCKET_RESIZE_NAME**: Nhập tên bucket, ví dụ **book-image-resize-stores-by-myself**.
      - **TABLE_NAME**: Nhập tên bảng, ví dụ **Books**.
    - Sau đó nhấn **Save**.
![CreateFunction](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/27.png?width=90pc)

7. Thêm những quyền cần thiết cho Lambda function để viết file vào S3 bucket.
    - Nhấn vào tab **Configuration**.
    - Chọn **Permissions** ở menu bên trái.
    - Nhấn vào role của function đang thực hiện.
![CreateFunction](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/28.png?width=90pc)

8. Ở trang **book_create-role-...**.
    - Chọn chính sách hiện có mà bắt đầu bằng **AWSLambdaExecutionRole-...**.
![CreateFunction](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/29.png?width=90pc)

9. Ở trang **AWSLambdaBasicExecutionRole-...**.
    - Nhấn vào **Edit**.
![CreateFunction](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/30.png?width=90pc)

10. Ở trang **Step 1: Modify permissions in AWSLambdaBasicExecutionRole-**.
    - Thêm đoạn code json sau vào **Policy editor**.
      ```
      {
                  "Effect": "Allow",
                  "Action": "s3:PutObject",
                  "Resource": "arn:aws:s3:::book-image-stores-by-myself/*"
              }
      ```
    - Nhấn vào **Next**.
![CreateFunction](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/31.png?width=90pc)

11. Ở trang **Step 2: Review and save**.
    - Xem lại cấu hình và bấm **Save changes**.
![CreateFunction](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/32.png?width=90pc)