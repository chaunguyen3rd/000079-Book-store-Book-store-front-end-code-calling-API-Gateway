---
title : "Liệt kê hàm Lambda"
date :  2025-02-11
weight : 2
chapter : false
pre : " <b> 3.2.2 </b> "
---
Chúng ta sẽ tạo một hàm Lambda để đọc tất cả dữ liệu trong bảng DynamoDB.

1. Mở [AWS Lambda console](https://us-east-1.console.aws.amazon.com/lambda/home?region=us-east-1#/functions).
    - Nhấp vào **Functions**.
    - Nhấp vào **Create function**.
      ![LambdaListFunction](/images/temp/1/33.png?width=90pc)

2. Tại trang **Create function**.
    - Nhập tên hàm, ví dụ: `books_list`.
    - Chọn **Python 3.11** cho mục **Runtime**.
    - Nhấp vào **Create function**.
      ![LambdaListFunction](/images/temp/1/34.png?width=90pc)

3. Tại trang **books_list**.
    - Sao chép đoạn mã dưới đây và dán vào **lambda_function.py**.

    ```python
    import boto3
    import os
    import simplejson as json

    TABLE = os.environ['TABLE_NAME']

    # Get the service resource
    dynamodb = boto3.resource('dynamodb')
    table = dynamodb.Table(TABLE)

    header_res = {
        "Content-Type": "application/json",
        "Access-Control-Allow-Origin": "*",
        "Access-Control-Allow-Methods": "OPTIONS,POST,GET,DELETE",
        "Access-Control-Allow-Headers": "Content-Type,X-Amz-Date,Authorization,X-Api-Key,X-Amz-Security-Token",
    }

    secondary_index = "name-index"


    def lambda_handler(event, context):
        try:
            books_data = table.scan(
                TableName=TABLE,
                IndexName=secondary_index
            )

            books = books_data.get('Items', [])

            for book in books:
                data_comment = table.query(
                    TableName=TABLE,
                    KeyConditionExpression="id = :id AND rv_id > :rv_id",
                    ExpressionAttributeValues={
                        ":id": book['id'],
                        ":rv_id": 0
                    }
                )

                book['comments'] = data_comment['Items']

            return {
                "statusCode": 200,
                "headers": header_res,
                "body": json.dumps(books, use_decimal=True)
            }
        except Exception as e:
            print(f'Error getting items: {e}')
            raise Exception(f'Error getting items: {e}')
    ```

    - Nhấp vào **Deploy**.
      ![LambdaListFunction](/images/temp/1/35.png?width=90pc)
    - Nhấp vào tab **Configuration**.
    - Nhấp vào **Environment variables** ở menu bên trái.
    - Nhấp vào **Edit**.
      ![LambdaListFunction](/images/temp/1/36.png?width=90pc)

4. Tại trang **Edit environment variables**.
    - Nhấp vào **Add environment variable**, sau đó thêm các biến môi trường sau:
      - `TABLE_NAME`: Nhập tên bảng, ví dụ `Books`.
    - Sau đó nhấp vào **Save**.
      ![LambdaListFunction](/images/temp/1/37.png?width=90pc)

5. Tiếp theo, cấp quyền cho hàm để đọc dữ liệu từ DynamoDB.
    - Nhấp vào tab **Configuration**.
    - Chọn mục **Permissions** ở menu bên trái.
    - Nhấp vào vai trò mà hàm đang thực thi.
      ![LambdaListFunction](/images/temp/1/38.png?width=90pc)

6. Tại trang **books_list-role-...**.
    - Nhấp vào chính sách hiện có bắt đầu bằng **AWSLambdaExecutionRole-**.
    - Nhấp vào **Edit**.
      ![LambdaListFunction](/images/temp/1/39.png?width=90pc)

7. Tại trang **Step 1: Modify permissions in AWSLambdaBasicExecutionRole-...**.
    - Thêm khối json dưới đây vào **Policy editor**:

      ```json
      {
                  "Effect": "Allow",
                  "Action": [
                      "dynamodb:Scan",
                      "dynamodb:Query"
                  ],
                  "Resource": "arn:aws:dynamodb:AWS_REGION:ACCOUNT_ID:table/Books"
              }
      ```

      - Thay thế **AWS_REGION** bằng vùng mà bạn tạo bảng trong DynamoDB, ví dụ: **us-east-1**.
      - Thay thế **ACCOUNT_ID** bằng id tài khoản của bạn.
    - Nhấp vào **Next**.
      ![LambdaListFunction](/images/temp/1/40.png?width=90pc)

8. Tại trang **Review and save**.
    - Nhấp vào **Save changes**.
      ![LambdaListFunction](/images/temp/1/41.png?width=90pc)
