---
title : "Triển khai front-end"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 2. </b> "
---
Bước đầu trong bài này, chúng ta sẽ host ứng dụng web (front-end) với S3 Static website hosting.

1. Mở bảng điều khiển [Amazon S3](https://s3.console.aws.amazon.com/s3/get-started?region=ap-southeast-2).
    - Nhấn vào **Buckets**.
    - Nhấn vào **Create bucket**. 
![S3Console](/images/temp/1/1.png?width=90pc)

2. Ở trang **Create bucket**.
    - Nhập tên bucket, ví dụ: **fcj-book-shop-by-myself**.
  ![S3Console](/images/temp/1/2.png?width=90pc)
    - Kéo xuống, bỏ chọn **Block all public access**.
    - Chọn **I acknowledge that the current settings might result in this bucket and the objects within becoming public.**.
  ![S3Console](/images/temp/1/3.png?width=90pc)
    - Kéo xuống, giữ mặc định và bấm nút **Create bucket**.
  ![S3Console](/images/temp/1/4.png?width=90pc)

3. Nhấn vào bucket **fcj-book-shop-by-myself**.
![S3Console](/images/temp/1/5.png?width=90pc)

4. Ở trang **fcj-book-shop-by-myself**.
    - Bấm vào tab **Properties**.
  ![S3Console](/images/temp/1/6.png?width=90pc)
    - Kéo xuống dưới cùng, bấm **Edit** ở mục **Static web hosting**.
  ![S3Console](/images/temp/1/7.png?width=90pc)
    - Ở trang **Edit static website hosting**.
      - Chọn **Enable** ở mục **Static website hosting**.
      - Chọn **Host a static website** ở mục **Hosting type**.
      - Nhập **index.html** at **Index document**.
    ![S3Console](/images/temp/1/8.png?width=90pc)
      - Kéo xuống, và bấm nút **Save changes**.
    ![S3Console](/images/temp/1/9.png?width=90pc)
    - Bấm vào tab **Permissions**.
    - Nhấn nút **Edit** ở mục **Bucket policy**.
  ![S3Console](/images/temp/1/10.png?width=90pc)

5. Ở trang **Edit bucket policy**.
    - Sao chép đoạn code dưới đây vào **Policy**.
    ```
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Sid": "PublicReadGetObject",
                "Effect": "Allow",
                "Principal": "*",
                "Action": "s3:GetObject",
                "Resource": "arn:aws:s3:::fcj-book-shop-by-myself/*"
            }
        ]
    }
    ```
    - Nhấn nút **Save changes**.
![S3Console](/images/temp/1/11.png?width=90pc)

6. Tải đoạn code **fcj-serverless-frontend** về máy của bạn.
    - Mở command-line/terminal ở đường dẫn bạn muốn lưu trữ source code.
    - Sao chép những câu lệnh bên dưới.
        ```
        git clone https://github.com/AWS-First-Cloud-Journey/FCJ-Serverless-Workshop.git
        cd FCJ-Serverless-Workshop
        yarn
        yarn build
        ```

7. Chúng ta đã hoàn thiện việc xây dựng front-end. Tiếp theo sẽ thực thi các câu lệnh để tải thư mục **build** lên S3.
    ```
    aws s3 cp build s3://fcj-book-shop-by-myself --recursive
    ```
  {{% notice note %}}
  Nếu quá trình tải lên của bạn không thành công, hãy cấu hình ID khóa truy cập, khóa truy cập bí mật, vùng aws và định dạng đầu ra bằng lệnh **aws configure**
  {{% /notice %}}
  Kết quả sau khi tải lên:
![S3Console](/images/temp/1/12.png?width=90pc)

8. Ở trang **fcj-book-shop-by-myself**.
    - Kéo xuống dưới cùng và lấy url từ **Bucket website endpoint**.
![S3Console](/images/temp/1/13.png?width=90pc)

9. Bấm vào url **http://fcj-book-shop-by-myself.s3-website-us-east-1.amazonaws.com** và kiểm tra kết quả.
![S3Console](/images/temp/1/14.png?width=90pc)

Ứng dụng của bạn hiện tại chưa có dữ liệu nào được trả về. Để lấy dữ liệu từ DynamoDB, hãy sang phần tiếp theo.


