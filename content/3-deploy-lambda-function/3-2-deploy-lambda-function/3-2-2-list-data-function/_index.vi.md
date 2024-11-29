---
title : "Lambda function đọc dữ liệu"
date :  "`r Sys.Date()`" 
weight : 2
chapter : false
pre : " <b> 3.2.2 </b> "
---
Chúng ta sẽ tạo một Lambda function đọc toàn bộ dữ liệu trong bảng của DynamoDB:
1. Ấn nút **Create function**
![LambdaListFunction](/images/1/25.png?width=90pc)

2. Nhập tên cho function, ví dụ: **books_list**
    - Chọn **Python 3.9** cho mục **Runtime**
    - Ấn nút **Create function**
![LambdaListFunction](/images/1/26.png?width=90pc)

3. Sao chép đoạn code dưới đây và dán vào mục **lambda_function.py**.
    ```
    import json
    import boto3
    from decimal import *
    from boto3.dynamodb.types import TypeDeserializer

    client = boto3.client('dynamodb') 
    serializer = TypeDeserializer()

    class DecimalEncoder(json.JSONEncoder):
        def default(self, obj):
            if isinstance(obj, Decimal):
                return str(obj)
            return json.JSONEncoder.default(self, obj)
                
    def deserialize(data):
        if isinstance(data, list):
            return [deserialize(v) for v in data]

        if isinstance(data, dict):
            try:
                return serializer.deserialize(data)
            except TypeError:
                return {k: deserialize(v) for k, v in data.items()}
        else:
            return data

    def lambda_handler(event, context):
        data_books = client.scan(
            TableName='Books',
            IndexName='name-index'
        )
        format_data_books = deserialize(data_books["Items"])
        for book in format_data_books:
            data_comment = client.query(
                TableName="Books", 
                KeyConditionExpression="id = :id AND rv_id > :rv_id", 
                ExpressionAttributeValues={
                    ":id": {"S": book['id']}, 
                    ":rv_id": {"N": "0"}
                }
            )
            format_data_comment = deserialize(data_comment['Items'])
            print(data_comment['Items'])
            book["comments"] = format_data_comment
                
        print (format_data_books)
        return {
            "statusCode": 200,
            "headers": {
                "Content-Type": "application/json",
                "Access-Control-Allow-Origin": "*",
                "Access-Control-Allow-Methods": "GET,PUT,POST,DELETE, OPTIONS",
                "Access-Control-Allow-Headers": "Access-Control-Allow-Headers, Origin,Accept, X-Requested-With, Content-Type, Access-Control-Request-Method,X-Access-Token,XKey,Authorization"
            },
            "body": json.dumps(format_data_books, cls=DecimalEncoder)
        }
    ```
    - Ấn nút **Deploy**
![LambdaListFunction](/images/1/27.png?width=90pc)

4. Tiếp theo, cấp quyền cho function có thể đọc được dữ liệu từ DynamoDB
    - Ấn sang tab **Configuration**
    - Chọn **Permissions** ở menu phía bên trái
    - Ấn vào role mà function đang thực hiện
![LambdaListFunction](/images/1/28.png?width=90pc)

    - Ấn vào policy có sẵn bắt đầu bằng **AWSLambdaExecutionRole-**
    - Ấn nút **Edit policy**
![LambdaListFunction](/images/1/29.png?width=90pc)
    - Ấn sang tab **JSON** và thêm đoạn json sau:
        ```
        ,
                {
                    "Effect": "Allow",
                    "Action": [
                        "dynamodb:Scan",
                        "dynamodb:Query"
                    ],
                    "Resource": "arn:aws:dynamodb:AWS_REGION:ACCOUNT_ID:table/Books"
                }
        ```
    - Thay **AWS_REGION** bằng vùng mà bạn tạo bảng trong DynamoDB, ví dụ: **ap-southeast-2**
    - Thay **ACCOUNT_ID** bằng id tài khoản của bạn.
    - Ấn nút **Review policy**
![LambdaListFunction](/images/1/30.png?width=90pc)

    - Xem lại các thiết lập và ấn **Save changes**
![LambdaListFunction](/images/1/31.png?width=90pc)

