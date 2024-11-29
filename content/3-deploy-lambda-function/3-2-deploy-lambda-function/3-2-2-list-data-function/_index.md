---
title : "Listing Lambda function"
date :  "`r Sys.Date()`" 
weight : 2
chapter : false
pre : " <b> 3.2.2 </b> "
---
We will create a Lambda function that reads all the data in the DynamoDB table:
1. Click **Create function**
![LambdaListFunction](/images/1/25.png?width=90pc)

2. Enter function name, such as: **books_list**
    - Select **Python 3.9** for **Runtime** pattern
    - Click **Create function**
![LambdaListFunction](/images/1/26.png?width=90pc)

3. Copy the below code block and paste to **lambda_function.py**.
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
    - Click **Deploy**
![LambdaListFunction](/images/1/27.png?width=90pc)

4. Next, give the function permission to read data from DynamoDB
    - Click **Configuration** tab
    - Select **Permissions** pattern on the left menu
    - Click on the role the function is executing
![LambdaListFunction](/images/1/28.png?width=90pc)

    - Click on the existing policy that starts with **AWSLambdaExecutionRole-**
    - Click **Edit policy**
![LambdaListFunction](/images/1/29.png?width=90pc)
    - Click **JSON** tab and add the below json block:
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
    - Replace **AWS_REGION** with the region where you create the table in DynamoDB, such as: **ap-southeast-2**
    - Replace **ACCOUNT_ID** with your account id
    - Click **Review policy**
![LambdaListFunction](/images/1/30.png?width=90pc)

    - Review the settings and click **Save changes**
![LambdaListFunction](/images/1/31.png?width=90pc)

