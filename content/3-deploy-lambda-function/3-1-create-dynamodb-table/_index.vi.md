---
title : "Tạo bảng DynamoDB"
date :  2025-02-11
weight : 1
chapter : false
pre : " <b> 3.1 </b> "
---

1. Mở [DynamoDB console](https://us-east-1.console.aws.amazon.com/dynamodbv2/home?region=us-east-1#dashboard).
    - Nhấp vào **Tables** ở menu bên trái.
    - Nhấp vào nút **Create table**.
      ![DynamoDBConsole](/images/temp/1/15.png?width=90pc)

2. Tại trang **Create table**.
    - Nhập tên bảng: ``Books``.
    - Nhập partition key: `id`.
    - Nhập sort key: `rv_id` (review id), loại là **Number**.
      ![DynamoDBConsole](/images/temp/1/16.png?width=90pc)
    - Cuộn xuống, chọn **Customize settings** tại **Table settings**.
    - Chọn **DynamoDB Standard** tại **Table class**.
    - Chọn **On-demand** tại **Read/write capacity settings**.
      ![DynamoDBConsole](/images/temp/1/17.png?width=90pc)
    - Cuộn xuống, nhấp vào **Create local index**.
      ![DynamoDBConsole](/images/temp/1/18.png?width=90pc)
    - Tại modal **New local secondary index**.
      - Nhập sort key: `name`.
      - Nhập index-name: `name-index`.
      - Nhấp vào nút **Create index**.
        ![DynamoDBConsole](/images/temp/1/19.png?width=90pc)
    - Cuộn xuống dưới cùng, nhấp vào nút **Create table**.
      ![DynamoDBConsole](/images/temp/1/20.png?width=90pc)

    Vậy là chúng ta đã tạo bảng **Books** với Local secondary index là **name-index**.

3. Để thêm dữ liệu vào bảng, bạn có thể tải xuống tệp dưới đây:
{{%attachments title="Data" pattern=".*\.(json)$"/%}}

4. Mở tệp này, thay thế tất cả **`<AWS-REGION>`** bằng vùng mà bạn đã tạo bucket S3 **book-image-resize-shop-by-myself**, ví dụ: **us-east-1**.
![DynamoDBConsole](/images/temp/1/21.png?width=90pc)

5. Chạy lệnh sau trong thư mục nơi bạn lưu dynamoDB.json

    ```bash
    aws dynamodb batch-write-item --request-items file://dynamoDB.json
    ```

    ![DynamoDBConsole](/images/temp/1/22.png?width=90pc)
