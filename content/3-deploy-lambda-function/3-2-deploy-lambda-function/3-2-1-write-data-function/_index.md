---
title : "Writing Lambda function"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 3.2.1 </b> "
---
In this step, we will update the code for the **book_create** created function in post 1:
1. Open [AWS Lambda console](https://ap-southeast-2.console.aws.amazon.com/lambda/home?region=ap-southeast-2#/functions), then Click **book_create** function
![LambdaConsole](/images/1/21.png?width=90pc)
3. Copy the below code block into **lambda_function.py**
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
    - Then, click **Deploy**
{{% notice note %}}
The new code handles the images that the user wants to upload and is saved in the S3 bucket
{{% /notice %}}
{{% notice warning %}}
If you create S3 buckets with names different from the lab, replace them in lines 35 and 36 of code
{{% /notice %}}

4. Give the Lambda function permission to write a file to the S3 bucket.
    - Click **Configuration** tab
    - Select **Permissions** pattern on the left menu
    - Click on the role the function is executing
![LambdaConsole](/images/1/22.png?width=90pc)

    - Click on the existing policy that starts with **AWSLambdaExecutionRole-**
    - Click **Edit policy**
    - Click **JSON** tab and add the blow json block:
        ```
        ,
                {
                    "Effect": "Allow",
                    "Action": "s3:PutObject",
                    "Resource": "arn:aws:s3:::book-image-store/*"
                }
        ```
        ![LambdaConsole](/images/1/23.png?width=90pc)
    - Click **Next**
    - Review the settings and click **Save changes**
![LambdaConsole](/images/1/24.png?width=90pc)




