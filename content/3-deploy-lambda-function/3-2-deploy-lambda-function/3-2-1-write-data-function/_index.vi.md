---
title : "Lambda function ghi dữ liệu"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 3.2.1 </b> "
---
Trong bước này chúng ta sẽ cập nhật lại code cho function **book_create** đã tạo ở bài số 1:

1. Mở bảng điều khiển của [AWS Lambda](https://ap-southeast-2.console.aws.amazon.com/lambda/home?region=ap-southeast-2#/functions), nhấn vào ***book_create** function đã tạo từ bài số 1
![LambdaConsole](/images/1/21.png?width=90pc)
3. Sao chép đoạn code sau vào mục **lambda_function.py**
        ```
        import boto3
        import json
        import base64
        import io
        import cgi
        import os

        s3 = boto3.client('s3')
        client = boto3.resource('dynamodb')
        runtime_region = os.environ['AWS_REGION']

        def get_data_from_request_body(content_type, body):
            fp = io.BytesIO(base64.b64decode(body)) # decode
            environ = {"REQUEST_METHOD": "POST"}
            headers = {
                "content-type": content_type,
                "content-length": len(body),
            }

            fs = cgi.FieldStorage(fp=fp, environ=environ, headers=headers) 
            return [fs, None]
            
        def lambda_handler(event, context):
            content_type = event['headers'].get('Content-Type', '') or event['headers'].get('content-type', '')
            
            if content_type == 'application/json':
                book_item = json.loads(event["body"])
            else:
                book_data, book_data_error = get_data_from_request_body(
                    content_type=content_type, body=event["body"]
                )
            
                name = book_data['image'].filename
                image = book_data['image'].value
                s3.put_object(Bucket='book-image-store', Key=name, Body=image)
                image_path = "https://{}.s3.{}.amazonaws.com/{}".format("book-image-resize-store", runtime_region, name)
                
                book_item = {
                    "id": book_data['id'].value,
                    "rv_id": 0,
                    "name": book_data['name'].value,
                    "author": book_data['author'].value,
                    "price" : book_data['price'].value,
                    "category": book_data['category'].value,
                    "description": book_data['description'].value,
                    "image": image_path
                }
            
            table = client.Table('Books')
            table.put_item(Item = book_item)
            
            response = {
                'statusCode': 200,
                'body': 'successfully created item!',
                'headers': {
                    'Content-Type': 'application/json',
                    "Access-Control-Allow-Headers": "Access-Control-Allow-Headers, Origin, Accept, X-Requested-With, Content-Type, Access-Control-Request-Method,X-Access-Token, XKey, Authorization",
                    "Access-Control-Allow-Origin": "*",
                    "Access-Control-Allow-Methods": "GET,PUT,POST,DELETE,OPTIONS"
                },
            }
        
            return response
        ```
    - Sau đó ấn **Deploy**
{{% notice note %}}
Code xử lý ảnh mà người dùng muốn tải lên và được lưu trong S3 bucket
{{% /notice %}}
{{% notice warning %}}
Nếu bạn tạo bộ chứa S3 có tên khác với lab, hãy thay chúng tại dòng 35 và 36 trong code
{{% /notice %}}

4. Cấp quyền cho Lambda function có thể ghi tệp vào S3 bucket.
    - Ấn sang tab **Configuration**
    - Chọn mục **Permissions** ở menu bên trái
    - Ấn vào role mà function đang thực hiện.
![LambdaConsole](/images/1/22.png?width=90pc)

    - Ấn vào policy có sẵn bắt đầu bằng **AWSLambdaExecutionRole-**
    - Ấn nút **Edit policy**
    - Ấn sang tab **JSON** và thêm đoạn json sau:
        ```
        ,
                {
                    "Effect": "Allow",
                    "Action": "s3:PutObject",
                    "Resource": "arn:aws:s3:::book-image-store/*"
                }
        ```
        ![LambdaConsole](/images/1/23.png?width=90pc)
    - Ấn nút **Review policy**
    - Xem lại các thiết lập và ấn **Save changes**
![LambdaConsole](/images/1/24.png?width=90pc)





