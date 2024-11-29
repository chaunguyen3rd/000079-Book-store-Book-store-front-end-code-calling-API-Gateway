---
title : "Front-end deployment"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 2. </b> "
---
In the first step in this workshop, we will host the web application (front-end) with S3 Static website hosting:
1. Open [Amazon S3 console](https://s3.console.aws.amazon.com/s3/get-started?region=ap-southeast-2), then Click **Create bucket** 
![S3Console](/images/1/1.png?width=90pc)

3. Enter bucket name, such as: **fcj-book-shop**
    - Select the region closest to you
![S3Console](/images/1/2.png?width=90pc)

4. Uncheck block from allowing public access
    - Check to **I acknowledge that the current settings might result in this bucket and the objects within becoming public**
![S3Console](/images/1/3.png?width=90pc)

5. Click **Create bucket** button
![S3Console](/images/1/4.png?width=90pc)
6. Click on created bucket, click **Properties** tab
![S3Console](/images/1/5.png?width=90pc)

8. Scroll down to the bottom, click **Edit** in **Static web hosting** pattern
![S3Console](/images/1/6.png?width=90pc)

9. Select **Enable** to enable host web static on S3
    - Select **Host a static website** for **Hosting type**
    - Enter **index.html** for **Index document** pattern
![S3Console](/images/1/7.png?width=90pc)

10. Click **Save changes**
    - After successfully enabling, please write down the path of the web
![S3Console](/images/1/8.png?width=90pc)

11. Select **Permissions** tab
    - Click **Edit** of **Bucket policy** pattern
![S3Console](/images/1/9.png?width=90pc)

12. Copy the below code block to **Policy**
    ```
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Sid": "PublicReadGetObject",
                "Effect": "Allow",
                "Principal": "*",
                "Action": "s3:GetObject",
                "Resource": "arn:aws:s3:::fcj-book-shop/*"
            }
        ]
    }
    ```
    - Click **Save changes**
![S3Console](/images/1/10.png?width=90pc)

13. Download **fcj-serverless-frontend** code to device
    - Open command-line/terminal in the folder where you want to save the source code
    - Copy the below commands
        ```
        git clone https://github.com/AWS-First-Cloud-Journey/FCJ-Serverless-Workshop.git
        cd FCJ-Serverless-Workshop
        npm install --force
        yarn build
        ```
14. We have finished building the front-end. Next execute the following command to upload the **build** folder to S3
    ```
    aws s3 cp build s3://fcj-book-shop --recursive
    ```
{{% notice note %}}
If your upload fails, configure the access key ID, secret access key, aws region and output format with **aws configure** command
{{% /notice %}}
Result after uploading:
![S3Console](/images/1/12.png?width=90pc)

15. Paste the web link you take notes into your web browser
![S3Console](/images/1/13.png?width=90pc)

Your application currently has no data returned. To get data from DynamoDB, go to the next section.