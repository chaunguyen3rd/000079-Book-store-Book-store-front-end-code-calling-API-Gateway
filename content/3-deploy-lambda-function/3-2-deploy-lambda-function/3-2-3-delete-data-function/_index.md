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
![LambdaDeleteFunction](/images/temp/1/33.png?width=90pc)

2. At **Create function** page.
    - Enter function name, such as: **book_delete**.
    - Select **Python 3.11** for **Runtime** pattern.
    - Click **Create function**.
![LambdaDeleteFunction](/images/temp/1/42.png?width=90pc)

3. At **book_delete** page.
    - Copy the below code block and paste to **lambda_function.py**.
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
    - Click **Deploy**
  ![LambdaDeleteFunction](/images/temp/1/43.png?width=90pc)
    - Click **Configuration** tab.
    - Click **Environment variables** on the left menu.
    - Click **Edit**.
  ![LambdaDeleteFunction](/images/temp/1/44.png?width=90pc)

4. At **Edit environment variables** page.
    - Click **Add environment variable**, then add the following environment variables:
      - **BUCKET_NAME**: enter the bucket name, such as **book-image-resize-stores-by-myself**.
      - **TABLE_NAME**: enter the table name, such as **Books**.
    - Then click **Save**.
![LambdaDeleteFunction](/images/temp/1/45.png?width=90pc)

5. Next, give the Lambda function permission to delete object from the S3 bucket and access to DynamoDB table.
    - Click **Configuration** tab.
    - Select **Permissions** pattern on the left menu.
    - Click on the role the function is executing.
![LambdaDeleteFunction](/images/temp/1/46.png?width=90pc)

6. At **book_delete-role-...** page.
    - Click on the existing policy that starts with **AWSLambdaExecutionRole-**.
    - Click **Edit**.
![LambdaDeleteFunction](/images/temp/1/47.png?width=90pc)

7. At **Step 1: Modify permissions in AWSLambdaBasicExecutionRole-...** page.
    - Add the below json block to **Policy editor**:
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
      - Replace **AWS_REGION** with the region where you create the table in DynamoDB, such as: **us-east-1**.
      - Replace **ACCOUNT_ID** with your account id.
    - Click **Next**.
![LambdaDeleteFunction](/images/temp/1/48.png?width=90pc)

8. At **Review and save** page.
    - Click **Save changes**.
![LambdaDeleteFunction](/images/temp/1/49.png?width=90pc)
