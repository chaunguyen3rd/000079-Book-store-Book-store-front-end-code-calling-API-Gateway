---
title : "Deleting Lambda function"
date :  "`r Sys.Date()`" 
weight : 3
chapter : false
pre : " <b> 3.2.3 </b> "
---
We will create a Lambda function that deletes all items with the specified partition key and sort key in the DynamoDB table. And delete the image file in the S3 bucket.

1. Open [AWS Lambda console](https://ap-southeast-2.console.aws.amazon.com/lambda/home?region=ap-southeast-2#/functions).
    - Click **Functions**.
    - Click **Create function**.
![LambdaListFunction](/images/temp/1/33.png?width=90pc)

2. At **Create function** page.
    - Enter function name, such as: **books_list**.
    - Select **Python 3.11** for **Runtime** pattern.
    - Click **Create function**.
![LambdaListFunction](/images/1/33.png?width=90pc)
3. Copy the below code block into **lambda_function.py**
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
    - Click **Deploy**
    ![LambdaListFunction](/images/1/34.png?width=90pc)
{{% notice warning %}}
If you create S3 bucket with name different from the lab, replace it in line 42 of code
{{% /notice %}}

4. Next, give the Lambda function permission to delete object from the S3 bucket and access to DynamoDB table.
    - Click **Configuration** tab
    - Select **Permissions** pattern on the left menu
    - Click on the role the function is executing
![LambdaListFunction](/images/1/35.png?width=90pc)

    - Click on the existing policy that starts with **AWSLambdaExecutionRole-**
    - Click **Edit policy**
![LambdaListFunction](/images/1/36.png?width=90pc)
    - Click **JSON** tab and add the blow json block:
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
    - Replace **AWS_REGION** with the region where you create the table in DynamoDB, such as: **ap-southeast-2**
    - Replace **ACCOUNT_ID** with your account id
    - Click **Review policy**
![LambdaListFunction](/images/1/37.png?width=90pc)

    - Review the settings and click **Save changes**
![LambdaListFunction](/images/1/38.png?width=90pc)

