---
title : "Xóa hàm Lambda"
date :  "`r Sys.Date()`" 
weight : 3
chapter : false
pre : " <b> 3.2.3 </b> "
---
Chúng ta sẽ tạo một hàm Lambda để xóa tất cả các mục với partition key và sort key được chỉ định trong bảng DynamoDB. Và xóa tệp hình ảnh trong bucket S3.

1. Mở [AWS Lambda console](https://us-east-1.console.aws.amazon.com/lambda/home?region=us-east-1#/functions).
    - Nhấp vào **Functions**.
    - Nhấp vào **Create function**.
      ![LambdaDeleteFunction](/images/temp/1/33.png?width=90pc)

2. Tại trang **Create function**.
    - Nhập tên hàm, ví dụ: `book_delete`.
    - Chọn **Python 3.11** cho mục **Runtime**.
    - Nhấp vào **Create function**.
      ![LambdaDeleteFunction](/images/temp/1/42.png?width=90pc)

3. Tại trang **book_delete**.
    - Sao chép đoạn mã dưới đây và dán vào **lambda_function.py**.

    ```py
    import boto3
    import os

    BUCKET = os.environ['BUCKET_NAME']
    TABLE = os.environ['TABLE_NAME']

    s3_client = boto3.client('s3')
    dynamodb = boto3.resource('dynamodb')
    table = dynamodb.Table(TABLE)

    header_res = {
        "Content-Type": "application/json",
        "Access-Control-Allow-Origin": "*",
        "Access-Control-Allow-Methods": "OPTIONS,POST,GET,DELETE",
        "Access-Control-Allow-Headers": "Content-Type,X-Amz-Date,Authorization,X-Api-Key,X-Amz-Security-Token",
    }


    def lambda_handler(event, context):
        delete_id = event.get('pathParameters', {})
        delete_id['rv_id'] = 0

        try:
            # Get item from id
            try:
                delete_item = table.get_item(Key=delete_id)
                image_path = delete_item['Item'].get('image', '')
                image_name = image_path.split('/')[-1]

            except Exception as e:
                print(f"Error getting item with that {delete_id['id']}")
                raise Exception(f"Error getting item with that {delete_id['id']}")

            # Delete item in DynamoDB and s3 bucket
            try:
                items_with_same_id = table.query(
                    TableName=TABLE,
                    ProjectionExpression='rv_id',
                    KeyConditionExpression='id = :id',
                    ExpressionAttributeValues={':id': delete_id['id']}
                )

                for item in items_with_same_id['Items']:
                    delete_id['rv_id'] = item['rv_id']
                    table.delete_item(Key=delete_id)

                s3_client.delete_object(Bucket=BUCKET, Key=image_name)

            except Exception as e:
                print(f"Error getting item with that {delete_id['id']}")
                raise Exception(f"Error getting item with that {delete_id['id']}")

            return {
                'statusCode': 200,
                'body': 'Successfully delete item!',
                'headers': header_res
            }

        except Exception as e:
            print(f'Error deleting item: {e}')
            raise Exception(f'Error deleting item: {e}')
    ```

    - Nhấp vào **Deploy**
      ![LambdaDeleteFunction](/images/temp/1/43.png?width=90pc)
    - Nhấp vào tab **Configuration**.
    - Nhấp vào **Environment variables** ở menu bên trái.
    - Nhấp vào **Edit**.
      ![LambdaDeleteFunction](/images/temp/1/44.png?width=90pc)

4. Tại trang **Edit environment variables**.
    - Nhấp vào **Add environment variable**, sau đó thêm các biến môi trường sau:
      - `BUCKET_NAME`: nhập tên bucket, ví dụ `book-image-resize-stores-by-myself`.
      - `TABLE_NAME`: nhập tên bảng, ví dụ `Books`.
    - Sau đó nhấp vào **Save**.
      ![LambdaDeleteFunction](/images/temp/1/45.png?width=90pc)

5. Tiếp theo, cấp quyền cho hàm Lambda để xóa đối tượng từ bucket S3 và truy cập vào bảng DynamoDB.
    - Nhấp vào tab **Configuration**.
    - Chọn mục **Permissions** ở menu bên trái.
    - Nhấp vào vai trò mà hàm đang thực thi.
      ![LambdaDeleteFunction](/images/temp/1/46.png?width=90pc)

6. Tại trang **book_delete-role-...**.
    - Nhấp vào chính sách hiện có bắt đầu bằng **AWSLambdaExecutionRole-**.
    - Nhấp vào **Edit**.
      ![LambdaDeleteFunction](/images/temp/1/47.png?width=90pc)

7. Tại trang **Step 1: Modify permissions in AWSLambdaBasicExecutionRole-...**.
    - Thêm khối json dưới đây vào **Policy editor**:

      ```json
      {
                  "Effect": "Allow",
                  "Action": [
                      "dynamodb:DeleteItem",
                      "dynamodb:GetItem",
                      "dynamodb:Query",
                      "s3:DeleteObject"
                  ],
                  "Resource": [
                      "arn:aws:dynamodb:AWS_REGION:ACCOUNT_ID:table/Books",
                      "arn:aws:s3:::book-image-resize-stores-by-myself/*"
                  ]
              }
      ```

      - Thay thế **AWS_REGION** bằng vùng mà bạn tạo bảng trong DynamoDB, ví dụ: **us-east-1**.
      - Thay thế **ACCOUNT_ID** bằng id tài khoản của bạn.
    - Nhấp vào **Next**.
      ![LambdaDeleteFunction](/images/temp/1/48.png?width=90pc)

8. Tại trang **Review and save**.
    - Nhấp vào **Save changes**.
      ![LambdaDeleteFunction](/images/temp/1/49.png?width=90pc)
