---
title : "Cleanup"
date :  2025-02-11
weight : 7
chapter : false
pre : " <b> 7. </b> "
---

1. Delete DynamoDB table.
    - Open [DynamoDB console](https://us-east-1.console.aws.amazon.com/dynamodbv2/home?region=us-east-1#dashboard).
    - Select **Tables** on the left menu.
    - Select **Books** table.
    - Click **Delete**.
    - Enter `confirm` and click **Delete**.

2. Delete S3 bucket
    - Open [S3 console](https://s3.console.aws.amazon.com/s3/buckets?region=us-east-1)
    - Select **book-image-resize-stores-by-myself** bucket.
    - Click **Empty**.
    - Enter `permanently delete` and click **Empty**.
    - Select **fcj-book-shop-by-myself** bucket.
    - Click **Empty**.
    - Enter `permanently delete` and click **Empty**.
    - Select **book-image-resize-stores-by-myself** bucket.
    - Click **Delete**.
    - Enter `book-image-resize-stores-by-myself` and click **Delete bucket**.
    - Select **book-image-stores-by-myself** bucket.
    - Click **Delete**.
    - Enter `book-image-stores-by-myself` and click **Delete bucket**.
    - Select **fcj-book-shop-by-myself** bucket.
    - Click **Delete**.
    - Enter `fcj-book-shop-by-myself` and click **Delete bucket**.

3. Delete REST API
    - Open [API Gateway console](https://us-east-1.console.aws.amazon.com/apigateway/main/apis?region=us-east-1#)
    - Select **fcj-serverless-api**.
    - Click **Delete**.
    - Enter `confirm` and click **Delete**.

4. Delete Lambda functions
    - Open [AWS Lambda console](https://us-east-1.console.aws.amazon.com/lambda/home?region=us-east-1#/functions)
    - Select **book_create** function.
    - Click **Actions**.
    - Click **Delete**.
    - Enter `confirm` and click **Delete**.
    - Similar to **resize_image**, **books_list**, **book_create**, **book_delete** function.
