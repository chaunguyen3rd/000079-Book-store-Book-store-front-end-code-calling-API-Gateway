---
title : "Front-end deployment"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 2. </b> "
---
In the first step in this workshop, we will host the web application (front-end) with S3 Static website hosting. 

1. Open [Amazon S3 console](https://s3.console.aws.amazon.com/s3/get-started?region=us-east-1).
    - Click **General purpose buckets** on the left menu.
    - Click **Create bucket**.
![S3Console](/images/temp/1/1.png?width=90pc)

2. At **Create bucket** page.
    - Enter bucket name, such as: `fcj-book-shop-by-myself`.
      ![S3Console](/images/temp/1/2.png?width=90pc)
    - Scroll down, uncheck the **Block all public access**.
    - Check to **I acknowledge that the current settings might result in this bucket and the objects within becoming public.**.
      ![S3Console](/images/temp/1/3.png?width=90pc)
    - Scroll down, leave as default and click **Create bucket** button.
      ![S3Console](/images/temp/1/4.png?width=90pc)

3. Click on **fcj-book-shop-by-myself** bucket.
    ![S3Console](/images/temp/1/5.png?width=90pc)

4. At **fcj-book-shop-by-myself** page.
    - Click **Properties** tab.
      ![S3Console](/images/temp/1/6.png?width=90pc)
    - Scroll down to the bottom, click **Edit** in **Static web hosting** pattern.
      ![S3Console](/images/temp/1/7.png?width=90pc)
    - At **Edit static website hosting** page.
      - Choose **Enable** at **Static website hosting** level.
      - Choose **Host a static website** at **Hosting type** level.
      - Enter `index.html` at **Index document**.
        ![S3Console](/images/temp/1/8.png?width=90pc)
      - Scroll down, and click **Save changes** button.
        ![S3Console](/images/temp/1/9.png?width=90pc)
    - Click **Permissions** tab.
    - Click **Edit** button at **Bucket policy** pattern.
      ![S3Console](/images/temp/1/10.png?width=90pc)

5. At **Edit bucket policy** page.
    - Copy the below code block to **Policy**.

    ```json
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Sid": "PublicReadGetObject",
                "Effect": "Allow",
                "Principal": "*",
                "Action": "s3:GetObject",
                "Resource": "arn:aws:s3:::fcj-book-shop-by-myself/*"
            }
        ]
    }
    ```

    - Click **Save changes** button.
      ![S3Console](/images/temp/1/11.png?width=90pc)

6. Download **fcj-serverless-frontend** code to your device.
    - Open command-line/terminal in the folder where you want to save the source code.
    - Copy the below commands.

        ```bash
        git clone https://github.com/AWS-First-Cloud-Journey/FCJ-Serverless-Workshop.git
        cd FCJ-Serverless-Workshop
        yarn
        yarn build
        ```

7. We have finished building the front-end. Next execute the following command to upload the **build** folder to S3.
  {{% notice note %}}
  If your upload fails, configure the access key ID, secret access key, aws region and output format with **aws configure** command
  {{% /notice %}}

    ```bash
    aws s3 cp build s3://fcj-book-shop-by-myself --recursive
    ```

    Result after uploading:
    ![S3Console](/images/temp/1/12.png?width=90pc)

8. At **fcj-book-shop-by-myself** page.
    - Click **Properties** tab.
      ![S3Console](/images/temp/1/6.png?width=90pc)
    - Scroll down to the bottom and get the url from **Bucket website endpoint**.
      ![S3Console](/images/temp/1/13.png?width=90pc)

9. Click on the **http://fcj-book-shop-by-myself.s3-website-us-east-1.amazonaws.com** url and check the result.
    ![S3Console](/images/temp/1/14.png?width=90pc)

Your application currently has no data returned. To get data from DynamoDB, go to the next section.