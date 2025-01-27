---
title : "Writing Lambda function"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 3.2.1 </b> "
---
In this step, we will update the code for the **book_create** created function in post 1:

1. Open [AWS Lambda console](https://us-east-1.console.aws.amazon.com/lambda/home?region=us-east-1#/functions).
    - Click **Functions**.
    - Choose **book_create** function.
![LambdaConsole](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/23.png?width=90pc)

2. Download source code file to your device.
{{%attachments title="Source code" pattern=".*\.(zip)$"/%}}

3. At **book_create** page.
    - Click **Upload from** button.
    - Choose **.zip file**.
![LambdaConsole](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/24.png?width=90pc)

4. At **Upload a .zip file** modal.
    - Click **Upload** button and select the downloaded source code file.
    - Click **Save**.
![LambdaConsole](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/25.png?width=90pc)

5. At **book_create** page.
    - Click **Configuration** tab.
    - Click **Environment variables** on the left menu.
    - Click **Edit**.
![CreateFunction](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/26.png?width=90pc)

6. At **Edit environment variables** page.
    - Click **Add environment variable**, then add the following environment variables:
      - **BUCKET_NAME**: enter the bucket name, such as **book-image-stores-by-myself**.
      - **BUCKET_RESIZE_NAME**: enter the bucket name, such as **book-image-resize-stores-by-myself**.
      - **TABLE_NAME**: enter the table name, such as **Books**.
    - Then click **Save**.
![CreateFunction](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/27.png?width=90pc)

7. Give the Lambda function permission to write a file to the S3 bucket.
    - Click **Configuration** tab.
    - Select **Permissions** pattern on the left menu.
    - Click on the role the function is executing.
![CreateFunction](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/28.png?width=90pc)

8. At **book_create-role-...** page.
    - Click on the existing policy that starts with **AWSLambdaExecutionRole-...**.
![CreateFunction](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/29.png?width=90pc)

9. At **AWSLambdaBasicExecutionRole-...** page.
    - Click **Edit**.
![CreateFunction](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/30.png?width=90pc)

10. At **Step 1: Modify permissions in AWSLambdaBasicExecutionRole-** page.
    - Add the below json block to **Policy editor**.

      ```json
      {
                  "Effect": "Allow",
                  "Action": "s3:PutObject",
                  "Resource": "arn:aws:s3:::book-image-stores-by-myself/*"
              }
      ```

    - Click **Next**.
![CreateFunction](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/31.png?width=90pc)

11. At **Step 2: Review and save** page.
    - Review the settings and click **Save changes**.
![CreateFunction](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/32.png?width=90pc)
