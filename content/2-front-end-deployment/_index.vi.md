---
title : "Triển khai front-end"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 2. </b> "
---
Bước đầu trong bài này, chúng ta sẽ host ứng dụng web (front-end) với S3 Static website hosting:

1. Mở bảng điều khiển [Amazon S3](https://s3.console.aws.amazon.com/s3/get-started?region=ap-southeast-2), nhấn **Create bucket**
![S3Console](/images/1/1.png?width=90pc)

3. Nhập tên cho bucket, ví dụ: **fcj-book-shop**
    - Chọn vùng gần bạn nhất
![S3Console](/images/1/2.png?width=90pc)


4. Bỏ chọn chặn cho phép truy cập public
    - Tích vào mục **I acknowledge that the current settings might result in this bucket and the objects within becoming public**
![S3Console](/images/1/3.png?width=90pc)
5. Nhấn nút **Create bucket**
![S3Console](/images/1/4.png?width=90pc)

6. Ấn vào bucket vừa tạo, nhấn vào tab **Properties**
![S3Console](/images/1/5.png?width=90pc)

8. Kéo xuống cuối trang, ấn **Edit** của mục **Static web hosting**
![S3Console](/images/1/6.png?width=90pc)

9. Chọn **Enable** để kích hoạt host web tĩnh trên S3
    - Chọn **Host a static website** cho **Hosting type**
    - Nhập **index.html** cho mục **Index document**
![S3Console](/images/1/7.png?width=90pc)

10. Ấn nút **Save changes**
    - Sau khi kích hoạt thành công, bạn hãy ghi lại đường dẫn của web
![S3Console](/images/1/8.png?width=90pc)

11. Sau đó, chúng ta cần thêm proxy cho S3 bucket để có thể truy cập được:
    - Chọn sang tab **Permissions**
    - Ấn nút **Edit** tại mục **Bucket policy**
![S3Console](/images/1/9.png?width=90pc)

12. Sao chép đoạn dưới đây vào mục **Policy**
    ```
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Sid": "PublicReadGetObject",
                "Effect": "Allow",
                "Principal": "*",
                "Action": "s3:GetObject",
                "Resource": "arn:aws:s3:::fcj-book-shop/*"
            }
        ]
    }
    ```
    - Ấn nút **Save changes**
![S3Console](/images/1/10.png?width=90pc)

13. Tải code **fcj-serverless-frontend** về máy của bạn
    - Mở command-line/terminal trên máy bạn tại thư mục bạn muốn lưu source code
    - Sao chép câu lệnh dưới đây
        ```
        git clone https://github.com/AWS-First-Cloud-Journey/FCJ-Serverless-Workshop.git
        cd fcj-serverless-frontend
        npm install
        yarn build
        ```
14. Chúng ta đã build xong front-end. Tiếp theo thực hiện câu lệnh sau để tải thư mục **build** lên S3
    ```
    aws s3 cp build s3://fcj-book-shop --recursive
    ```
{{% notice note %}}
Nếu bạn tải lên thất bại, hãy cấu hình access key ID, secret access key, aws region và output format với câu lệnh **aws configure**
{{% /notice %}}
Kết quả sau khi tải xong:
![S3Console](/images/1/12.png?width=90pc)

15. Dán đường dẫn web mà bạn vừa ghi lại vào trình duyệt web của bạn
![S3Console](/images/1/13.png?width=90pc)
Ứng dụng của bạn hiện tại chưa có dữ liệu nào được trả về. Để lấy dữ liệu từ DynamoDB, hãy sang phần tiếp theo.


