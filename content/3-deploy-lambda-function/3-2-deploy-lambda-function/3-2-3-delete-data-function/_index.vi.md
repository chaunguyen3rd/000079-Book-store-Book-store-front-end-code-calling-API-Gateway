---
title : "Lambda function xoá dữ liệu"
date :  "`r Sys.Date()`" 
weight : 3
chapter : false
pre : " <b> 3.2.3 </b> "
---
Chúng ta sẽ tạo một Lambda function xoá toàn bộ item có partition key và sort key được chỉ định trong bảng của DynamoDB. Và xoá cả tệp ảnh trong S3 bucket:
1. Ấn nút **Create function**
![LambdaListFunction](/images/1/32.png?width=90pc)

2. Nhập tên cho function, ví dụ: **book_delete**
    - Chọn **Python 3.9** cho mục **Runtime**
    - Ấn nút **Create function**
![LambdaListFunction](/images/1/33.png?width=90pc)

3. Sao chép đoạn code dưới đây và dán vào mục **lambda_function.py**.
    ```
    import boto3
    import json

    s3 = boto3.client('s3')
    client = boto3.resource('dynamodb')

    def get_image_name(image_path):
        str_image = image_path.split("/")
        for image_path_item in str_image:
            image_name = image_path_item
            
        return image_name;
        
    def lambda_handler(event, context):
        error = None
        status = 200
        delete_id = event['pathParameters']
        delete_id['rv_id'] = 0
        
        table = client.Table("Books")
        image_path = ""

        try:
            data = table.get_item(Key = delete_id)
            image_path = data['Item']['image']
            image_name = get_image_name(image_path)
        except Exception as e:
            error = e
        
        try:
            response = table.query(
                ProjectionExpression="rv_id", 
                KeyConditionExpression="id = :id", 
                ExpressionAttributeValues={":id": delete_id['id']})
                
            for item in response['Items']:
                delete_id['rv_id'] = item['rv_id']
                print(delete_id)
                table.delete_item(Key = delete_id)
            
            print(image_name)
            s3.delete_object(Bucket='book-image-resize-store', Key=image_name)
            
        except Exception as e:
            error = e
        
        if error is None:
            message = 'successfully deleted item!'
        else:
            message = 'delete item fail'
            status = 400

        return {
                'statusCode': status,
                'body': message,
                'headers': {
                    'Content-Type': 'application/json',
                    'Access-Control-Allow-Origin': '*'
                },
            }
    ```
    - Ấn nút **Deploy**
 ![LambdaListFunction](/images/1/34.png?width=90pc)

4. Tiếp theo, cấp quyền cho function có thể đọc được dữ liệu từ DynamoDB và xoá object trong S3 bucket
    - Ấn sang tab **Configuration**
    - Chọn **Permissions** ở menu phía bên trái
    - Ấn vào role mà function đang thực hiện
![LambdaListFunction](/images/1/35.png?width=90pc)

    - Ấn vào policy có sẵn bắt đầu bằng **AWSLambdaExecutionRole-**
    - Ấn nút **Edit policy**
![LambdaListFunction](/images/1/36.png?width=90pc)

    - Ấn sang tab **JSON** và thêm đoạn json sau:
    ```
    ,
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
                    "arn:aws:s3:::book-image-resize-store/*"
                ]
            }
    ```
    - Thay **AWS_REGION** bằng vùng mà bạn tạo bảng trong DynamoDB, ví dụ: **ap-southeast-2**
    - Thay **ACCOUNT_ID** bằng id tài khoản của bạn.
    - Ấn nút **Review policy**
![LambdaListFunction](/images/1/37.png?width=90pc)

    - Xem lại các thiết lập và ấn **Save changes**
![LambdaListFunction](/images/1/38.png?width=90pc)
