---
title : "Listing Lambda function"
date :  "`r Sys.Date()`" 
weight : 2
chapter : false
pre : " <b> 3.2.2 </b> "
---
We will create a Lambda function that reads all the data in the DynamoDB table.
1. Open [AWS Lambda console](https://ap-southeast-2.console.aws.amazon.com/lambda/home?region=ap-southeast-2#/functions).
    - Click **Functions**.
    - Click **Create function**.
![LambdaListFunction](/images/temp/1/33.png?width=90pc)

2. At **Create function** page.
    - Enter function name, such as: **books_list**.
    - Select **Python 3.11** for **Runtime** pattern.
    - Click **Create function**.
![LambdaListFunction](/images/temp/1/34.png?width=90pc)

3. At **books_list** page.
    - Copy the below code block and paste to **lambda_function.py**.
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
    - Click **Deploy**
  ![LambdaListFunction](/images/temp/1/35.png?width=90pc)
    - Click **Configuration** tab.
    - Click **Environment variables** on the left menu.
    - Click **Edit**.
  ![LambdaListFunction](/images/temp/1/36.png?width=90pc)

4. At **Edit environment variables** page.
    - Click **Add environment variable**, then add the following environment variables:
      - **TABLE_NAME**: enter the table name, such as **Books**.
    - Then click **Save**.
![LambdaListFunction](/images/temp/1/37.png?width=90pc)

5. Next, give the function permission to read data from DynamoDB
    - Click **Configuration** tab
    - Select **Permissions** pattern on the left menu
    - Click on the role the function is executing
  ![LambdaListFunction](/images/temp/1/38.png?width=90pc)

6. At **books_list-role-...** page.
    - Click on the existing policy that starts with **AWSLambdaExecutionRole-**
    - Click **Edit policy**.
![LambdaListFunction](/images/temp/1/39.png?width=90pc) 

7. At **Step 1: Modify permissions in AWSLambdaBasicExecutionRole-...** page.
    - Add the below json block to **Policy editor**:
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
    - Replace **AWS_REGION** with the region where you create the table in DynamoDB, such as: **us-east-1**.
    - Replace **ACCOUNT_ID** with your account id.
    - Click **Next**.
![LambdaListFunction](/images/temp/1/40.png?width=90pc)

8. At **Review and save** page.
    - Click **Save changes**.
![LambdaListFunction](/images/temp/1/41.png?width=90pc)
    

