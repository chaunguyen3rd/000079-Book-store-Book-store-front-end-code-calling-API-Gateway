---
title : "Triển khai front-end"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 2. </b> "
---
Trong bước đầu tiên của workshop này, chúng ta sẽ lưu trữ ứng dụng web (front-end) với S3 Static website hosting.

1. Mở [Amazon S3 console](https://s3.console.aws.amazon.com/s3/get-started?region=us-east-1).
    - Nhấp vào **General purpose buckets** ở menu bên trái.
    - Nhấp vào **Create bucket**.
![S3Console](/images/temp/1/1.png?width=90pc)

2. Tại trang **Create bucket**.
    - Nhập tên bucket, ví dụ: `fcj-book-shop-by-myself`.
      ![S3Console](/images/temp/1/2.png?width=90pc)
    - Cuộn xuống, bỏ chọn **Block all public access**.
    - Chọn **I acknowledge that the current settings might result in this bucket and the objects within becoming public.**.
      ![S3Console](/images/temp/1/3.png?width=90pc)
    - Cuộn xuống, để mặc định và nhấp vào nút **Create bucket**.
      ![S3Console](/images/temp/1/4.png?width=90pc)

3. Nhấp vào bucket **fcj-book-shop-by-myself**.
    ![S3Console](/images/temp/1/5.png?width=90pc)

4. Tại trang **fcj-book-shop-by-myself**.
    - Nhấp vào tab **Properties**.
      ![S3Console](/images/temp/1/6.png?width=90pc)
    - Cuộn xuống dưới cùng, nhấp vào **Edit** trong phần **Static web hosting**.
      ![S3Console](/images/temp/1/7.png?width=90pc)
    - Tại trang **Edit static website hosting**.
      - Chọn **Enable** tại mục **Static website hosting**.
      - Chọn **Host a static website** tại mục **Hosting type**.
      - Nhập `index.html` tại mục **Index document**.
        ![S3Console](/images/temp/1/8.png?width=90pc)
      - Cuộn xuống và nhấp vào nút **Save changes**.
        ![S3Console](/images/temp/1/9.png?width=90pc)
    - Nhấp vào tab **Permissions**.
    - Nhấp vào nút **Edit** tại phần **Bucket policy**.
      ![S3Console](/images/temp/1/10.png?width=90pc)

5. Tại trang **Edit bucket policy**.
    - Sao chép đoạn mã dưới đây vào **Policy**.

    ```json
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

    - Nhấp vào nút **Save changes**.
      ![S3Console](/images/temp/1/11.png?width=90pc)

6. Tải mã nguồn **fcj-serverless-frontend** về thiết bị của bạn.
    - Mở dòng lệnh/terminal trong thư mục nơi bạn muốn lưu mã nguồn.
    - Sao chép các lệnh dưới đây.

        ```bash
        git clone https://github.com/AWS-First-Cloud-Journey/FCJ-Serverless-Workshop.git
        cd FCJ-Serverless-Workshop
        yarn
        yarn build
        ```

7. Chúng ta đã hoàn thành việc xây dựng front-end. Tiếp theo, thực hiện lệnh sau để tải thư mục **build** lên S3.
  {{% notice note %}}
  Nếu tải lên thất bại, cấu hình access key ID, secret access key, aws region và output format với lệnh **aws configure**.
  {{% /notice %}}

    ```bash
    aws s3 cp build s3://fcj-book-shop-by-myself --recursive
    ```

    Kết quả sau khi tải lên:
    ![S3Console](/images/temp/1/12.png?width=90pc)

8. Tại trang **fcj-book-shop-by-myself**.
    - Nhấp vào tab **Properties**.
      ![S3Console](/images/temp/1/6.png?width=90pc)
    - Cuộn xuống dưới cùng và lấy url từ **Bucket website endpoint**.
      ![S3Console](/images/temp/1/13.png?width=90pc)

9. Nhấp vào url <http://fcj-book-shop-by-myself.s3-website-us-east-1.amazonaws.com> và kiểm tra kết quả.
    ![S3Console](/images/temp/1/14.png?width=90pc)

Ứng dụng của bạn hiện tại chưa có dữ liệu trả về. Để lấy dữ liệu từ DynamoDB, hãy chuyển sang phần tiếp theo.
