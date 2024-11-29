---
title : "Tạo bảng trong DynamoDB"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 3.1 </b> "
---
1. Mở bảng điều khiển [DynamoDB](https://ap-southeast-1.console.aws.amazon.com/dynamodbv2/home?region=ap-southeast-1#dashboard), sau đó nhấn nút **Create table**
![DynamoDBConsole](/images/1/14.png?width=90pc)
3. Nhập tên cho bảng: **Books**
- Nhập parition key: `id`
- Nhập sort key: `rv_id` (review id), kiểu **Number**
![DynamoDBConsole](/images/1/15.png?width=90pc)

4. Kéo xuống phần **Table settings**, chọn **Customize settings**
- Sau đó, chọn **On-demand**
- Ấn nút **Create local Index**
![DynamoDBConsole](/images/1/16.png?width=90pc)

5. Nhập sort key: **name**
- Nhập index-name: **name-index**
- Ấn nút **Create index**
![DynamoDBConsole](/images/1/17.png?width=90pc)

6. Kéo xuống cuối trang, ấn nút **Create table**
![DynamoDBConsole](/images/1/18.png?width=90pc)
Vậy là bạn đã tạo xong bảng **Books** với Local secondary index là **name-index**

7. Để thêm dữ liệu cho bảng, bạn có thể tải tệp dưới đây:
{{%attachments title="Data" pattern=".*\.(json)$"/%}}

8. Mở tệp, sau đó thay toàn bộ **`<AWS-REGION>`** bằng vùng mà bạn tạo S3 bucket **book-image-resize-shop**, ví dụ: **ap-southeast-2**
![DynamoDBConsole](/images/1/19.png?width=90pc)
9. Chạy câu lệnh sau tại thư mục mà bạn lưu tệp dynamoDB.json
    ```
    aws dynamodb batch-write-item --request-items file://dynamoDB.json
    ```
    ![DynamoDBConsole](/images/1/20.png?width=90pc)