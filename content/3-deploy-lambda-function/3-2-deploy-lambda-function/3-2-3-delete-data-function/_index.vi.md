---
title : "Lambda function xoá dữ liệu"
date :  "`r Sys.Date()`" 
weight : 3
chapter : false
pre : " <b> 3.2.3 </b> "
---
Chúng ta sẽ tạo một Lambda function xoá toàn bộ item có partition key và sort key được chỉ định trong bảng của DynamoDB. Và xoá cả tệp ảnh trong S3 bucket.

1. Mở cửa sổ console [AWS Lambda console](https://ap-southeast-2.console.aws.amazon.com/lambda/home?region=ap-southeast-2#/functions).
    - Nhấn vào **Functions**.
    - Nhấn vào **Create function**.
![LambdaDeleteFunction](/images/temp/1/33.png?width=90pc)

2. Ở trang **Create function**.
    - Nhập tên function, ví dụ: **book_delete**.
    - Chọn **Python 3.11** cho **Runtime**.
    - Nhấn nút **Create function**.
![LambdaDeleteFunction](/images/temp/1/42.png?width=90pc)

3. Ở trang **book_delete**.
    - Sao chép đoạn code sau và dán vào **lambda_function.py**.
    ```
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
    - Nhấn **Deploy**.
  ![LambdaDeleteFunction](/images/temp/1/43.png?width=90pc)
    - Nhấn vào tab **Configuration**.
    - Nhấn **Environment variables** ở menu bên trái.
    - Nhấn **Edit**.
  ![LambdaDeleteFunction](/images/temp/1/44.png?width=90pc)

4. Ở trang **Edit environment variables**.
    - Nhấn vào **Add environment variable**, sau đó thêm vào biến môi trường:
      - **BUCKET_NAME**: Nhập tên bucket, ví dụ **book-image-resize-stores-by-myself**.
      - **TABLE_NAME**: Nhập tên bảng, ví dụ **Books**.
    - Then click **Save**.
![LambdaDeleteFunction](/images/temp/1/45.png?width=90pc)

5. Tiếp theo, thêm quyền cho function để có thể xóa đối tượng ở bucket S3 và truy cập vào bảng DynamoDB.
    - Nhấn vào tab **Configuration**.
    - Chọn **Permissions** ở menu bên trái.
    - Bấm vào role mà function đang thực thi.
![LambdaDeleteFunction](/images/temp/1/46.png?width=90pc)

6. Ở trang **book_delete-role-...**.
    - Bấm vào chính sách hiện tại bắt đầu bằng **AWSLambdaExecutionRole-**.
    - Nhấn vào **Edit**.
![LambdaDeleteFunction](/images/temp/1/47.png?width=90pc)

7. Ở trang **Step 1: Modify permissions in AWSLambdaBasicExecutionRole-...**.
    - Thêm đoạn code json vào **Policy editor**:
      ```
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
      - Thay thế **AWS_REGION** bằng region bạn đã tạo bảng, ví dụ: **us-east-1**.
      - Thay thế **ACCOUNT_ID** bằng id tài khoản của bạn.
    - Nhấn vào **Next**.
![LambdaDeleteFunction](/images/temp/1/48.png?width=90pc)

8. Ở trang **Review and save**.
    - Nhấn vào **Save changes**.
![LambdaDeleteFunction](/images/temp/1/49.png?width=90pc)
