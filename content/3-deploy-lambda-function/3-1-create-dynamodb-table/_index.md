---
title : "Create DynamoDB table"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 3.1 </b> "
---
1. Open [DynamoDB console](https://ap-southeast-1.console.aws.amazon.com/dynamodbv2/home?region=ap-southeast-1#dashboard).
    - Click **Tables**.
    - Click **Create table**.
![DynamoDBConsole](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/15.png?width=90pc)

2. At **Create table** page.
    - Enter table name: **Books**.
    - Enter partition key: `id`.
    - Enter sort key: `rv_id` (review id), type is **Number**.
  ![DynamoDBConsole](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/16.png?width=90pc)
    - Scroll down, select **Customize settings** at **Table settings**.
    - Select **DynamoDB Standard** at **Table class**.
    - Select **On-demand** at **Read/write capacity settings**.
  ![DynamoDBConsole](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/17.png?width=90pc)
    - Scroll down, click **Create local index**.
  ![DynamoDBConsole](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/18.png?width=90pc)
    - At **New local secondary index** modal.
      - Enter sort key: **name**.
      - Enter index-name: **name-index**.
      - Click **Create index**.
    ![DynamoDBConsole](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/19.png?width=90pc)
    - Scroll down to the bottom, click **Create table**.
    ![DynamoDBConsole](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/20.png?width=90pc)

    So we have created the **Books** table with the Local secondary index of **name-index**.

3. To add data to the table, you can download the file below:
{{%attachments title="Data" pattern=".*\.(json)$"/%}}

4. Open this file, replace all **`<AWS-REGION>`** with the region where you created the S3 **book-image-resize-shop-by-myself** bucket, for example: **us-east-1**.
![DynamoDBConsole](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/21.png?width=90pc)

5. Run the following command in the directory where you save the dynamoDB.json

    ```bash
    aws dynamodb batch-write-item --request-items file://dynamoDB.json
    ```

    ![DynamoDBConsole](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/22.png?width=90pc)
