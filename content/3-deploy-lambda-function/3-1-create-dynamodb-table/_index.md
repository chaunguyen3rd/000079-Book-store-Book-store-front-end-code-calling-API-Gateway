---
title : "Create DynamoDB table"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 3.1 </b> "
---
1. Open [DynamoDB console](https://ap-southeast-1.console.aws.amazon.com/dynamodbv2/home?region=ap-southeast-1#dashboard), then Click **Create table**
![DynamoDBConsole](/images/1/14.png?width=90pc)

3. Enter table name: **Books**
    - Enter parition key: `id`
    - Enter sort key: `rv_id` (review id), type is **Number**
![DynamoDBConsole](/images/1/15.png?width=90pc)

4. Scroll down to **Table settings** pattern, select **Customize settings**
    - Then, select **On-demand**
    - Click **Create local Index**
![DynamoDBConsole](/images/1/16.png?width=90pc)

5. Enter sort key: **name**
    - Enter index-name: **name-index**
    - Click **Create index**
![DynamoDBConsole](/images/1/17.png?width=90pc)

6. Scroll down to the bottom, click **Create table**
![DynamoDBConsole](/images/1/18.png?width=90pc)
So we have created the **Books** table with the Local secondary index of **name-index**

7. To add data to the table, you can download the file below:
{{%attachments title="Data" pattern=".*\.(json)$"/%}}

8. Open this file, replace all **`<AWS-REGION>`** with the region where you created the S3 **book-image-resize-shop** bucket, for example: **ap-southeast-2**
![DynamoDBConsole](/images/1/19.png?width=90pc)
9. Run the following command in the directory where you save the dynamoDB.json
    ```
    aws dynamodb batch-write-item --request-items file://dynamoDB.json
    ```
    ![DynamoDBConsole](/images/1/20.png?width=90pc)