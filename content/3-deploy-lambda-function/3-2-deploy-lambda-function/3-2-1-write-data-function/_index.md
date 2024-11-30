---
title : "Writing Lambda function"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 3.2.1 </b> "
---
In this step, we will update the code for the **book_create** created function in post 1:

1. Open [AWS Lambda console](https://ap-southeast-2.console.aws.amazon.com/lambda/home?region=ap-southeast-2#/functions).
    - Click **Functions**.
    - Choose **book_create** function.
![LambdaConsole](/images/temp/1/23.png?width=90pc)

2. Download source code file to your device 
{{%attachments title="Source code" pattern=".*\.(zip)$"/%}}

4. At **resize-image** page.
    - Click **Upload from** button.
    - Choose **.zip file**.
![CreateFunction](/images/temp/1/3.png?width=90pc)

5. At **Upload a .zip file** modal.
    - Click **Upload** button and select the downloaded source code file.
    - Click **Save**.
![CreateFunction](/images/temp/1/4.png?width=90pc)

6. At **resize-image** page.
    - Click **Configuration** tab.
    - Click **Environment variables** on the left menu.
    - Click **Edit**.
![CreateFunction](/images/temp/1/5.png?width=90pc)

7. At **Edit environment variables** page.
    - Click **Add environment variable**, then add the following environment variables:
      - **WIDTH**: enter the new width of the photo, such as 200px.
      - **HEIGHT**: enter the new hight of the photo, such as 280px.
      - **DES_BUCKET**: S3 bucket name to store the changed image, such as: **book-image-resize-stores-by-myself**.
    - Then click **Save**.
![CreateFunction](/images/temp/1/6.png?width=90pc)

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




