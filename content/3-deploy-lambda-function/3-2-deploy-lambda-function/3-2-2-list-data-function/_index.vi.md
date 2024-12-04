---
title : "Lambda function đọc dữ liệu"
date :  "`r Sys.Date()`" 
weight : 2
chapter : false
pre : " <b> 3.2.2 </b> "
---
Chúng ta sẽ tạo một Lambda function đọc toàn bộ dữ liệu trong bảng của DynamoDB:

1. Mở cửa sổ console [AWS Lambda console](https://ap-southeast-2.console.aws.amazon.com/lambda/home?region=ap-southeast-2#/functions).
    - Nhất vào **Functions**.
    - Nhất vào **Create function**.
![LambdaListFunction](/images/temp/1/33.png?width=90pc)

2. Ở trang **Create function**.
    - Nhập tên function, ví dụ: **books_list**.
    - Chọn **Python 3.11** cho **Runtime**.
    - Nhấn nút **Create function**.
![LambdaListFunction](/images/temp/1/34.png?width=90pc)

3. Ở trang **books_list**.
    - Sao chép đoạn code sau và dán vào **lambda_function.py**.
    ```
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
    - Nhấn **Deploy**.
  ![LambdaListFunction](/images/temp/1/35.png?width=90pc)
    - Nhấn vào tab **Configuration**.
    - Nhấn vào **Environment variables** ở menu bên trái.
    - Nhấn vào **Edit**.
  ![LambdaListFunction](/images/temp/1/36.png?width=90pc)

4. Ở trang **Edit environment variables**.
    - Nhấn vào **Add environment variable**, sau đó thêm vào biến môi trường:
      - **TABLE_NAME**: Nhập tên bảng, ví dụ **Books**.
    - Sau đó bấm **Save**.
![LambdaListFunction](/images/temp/1/37.png?width=90pc)

5. Tiếp theo, thêm quyền cho function để có thể đọc dữ liệu từ DynamoDB.
    - Bấm vào tab **Configuration**.
    - Chọn **Permissions** ở menu bên trái.
    - Bấm vào role mà function đang thực thi.
  ![LambdaListFunction](/images/temp/1/38.png?width=90pc)

6. Ở trang **books_list-role-...**.
    - Bấm vào chính sách hiện tại bắt đầu bằng **AWSLambdaExecutionRole-**.
    - Bấm vào **Edit**.
![LambdaListFunction](/images/temp/1/39.png?width=90pc) 

7. Ở trang **Step 1: Modify permissions in AWSLambdaBasicExecutionRole-...**.
    - Thêm đoạn code json vào **Policy editor**:
      ```
      {
                  "Effect": "Allow",
                  "Action": [
                      "dynamodb:Scan",
                      "dynamodb:Query"
                  ],
                  "Resource": "arn:aws:dynamodb:AWS_REGION:ACCOUNT_ID:table/Books"
              }
      ```
      - Thay thế **AWS_REGION** bằng region bạn đã tạo bảng, ví dụ: **us-east-1**.
      - Thay thế **ACCOUNT_ID** bằng id tài khoản của bạn.
    - Nhấn vào **Next**.
![LambdaListFunction](/images/temp/1/40.png?width=90pc)

8. Ở trang **Review and save**.
    - Nhấn vào **Save changes**.
![LambdaListFunction](/images/temp/1/41.png?width=90pc)