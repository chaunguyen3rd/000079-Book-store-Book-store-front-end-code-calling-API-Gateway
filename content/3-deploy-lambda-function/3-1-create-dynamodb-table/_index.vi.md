---
title : "Tạo bảng trong DynamoDB"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 3.1 </b> "
---
1. Mở bảng điều khiển [DynamoDB console](https://ap-southeast-1.console.aws.amazon.com/dynamodbv2/home?region=ap-southeast-1#dashboard).
    - Nhấn vào **Tables**.
    - Nhấn vào **Create table**.
![DynamoDBConsole](/images/temp/1/15.png?width=90pc)

2. Ở trang **Create table**.
    - Nhập tên cho bảng: **Books**.
    - Nhập parition key: `id`.
    - Nhập sort key: `rv_id` (review id), kiểu **Number**.
  ![DynamoDBConsole](/images/temp/1/16.png?width=90pc)
    - Kéo xuống, chọn **Customize settings** ở **Table settings**.
    - Chọn **DynamoDB Standard** ở **Table class**.
    - Chọn **On-demand** ở **Read/write capacity settings**.
  ![DynamoDBConsole](/images/temp/1/17.png?width=90pc)
    - Kéo xuống, bấm vào **Create local index**.
  ![DynamoDBConsole](/images/temp/1/18.png?width=90pc)
    - Ở hộp thoại **New local secondary index**.
      - Nhập sort key: **name**.
      - Nhập index-name: **name-index**.
      - Bấm vào **Create index**.
    ![DynamoDBConsole](/images/temp/1/19.png?width=90pc)
    - Kéo xuống dưới cùng, bấm vào **Create table**.
    ![DynamoDBConsole](/images/temp/1/20.png?width=90pc)

    Vậy là bạn đã tạo xong bảng **Books** với Local secondary index là **name-index**.

3. Để thêm dữ liệu cho bảng, bạn có thể tải tệp dưới đây:
{{%attachments title="Data" pattern=".*\.(json)$"/%}}

4. Mở tệp, sau đó thay toàn bộ **`<AWS-REGION>`** bằng vùng mà bạn tạo S3 bucket **book-image-resize-shop-by-myself**, ví dụ: **us-east-1**.
![DynamoDBConsole](/images/temp/1/21.png?width=90pc)

5. Chạy câu lệnh sau tại thư mục mà bạn lưu tệp dynamoDB.json
    ```
    aws dynamodb batch-write-item --request-items file://dynamoDB.json
    ```
![DynamoDBConsole](/images/temp/1/22.png?width=90pc)