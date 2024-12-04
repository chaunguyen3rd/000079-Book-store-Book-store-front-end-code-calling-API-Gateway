---
title : "Dọn dẹp tài nguyên"
date :  "`r Sys.Date()`" 
weight : 7
chapter : false
pre : " <b> 7. </b> "
---

1. Xoá bảng trong DynamoDB
- Mở bảng điều khiển của [DynamoDB](https://ap-southeast-2.console.aws.amazon.com/dynamodbv2/home?region=ap-southeast-2#dashboard).
- Chọn **Tables** ở menu phía bên trái.
- Chọn bảng **Books**.
- Ấn **Delete**.
- Nhập **confirm** và ấn **Delete**.

2. Xoá S3 bucket
- Mở bảng điều khiển của [S3](https://s3.console.aws.amazon.com/s3/buckets?region=ap-southeast-2).
- Chọn bucket **book-image-resize-stores-by-myself**.
- Ấn nút **Empty**.
- Nhập **permanently delete** và ấn **Empty**.
- Chọn bucket **fcj-book-shop-by-myself**.
- Ấn nút **Empty**.
- Nhập **permanently delete** và ấn **Empty**.
- Chọn bucket **book-image-resize-stores-by-myself**.
- Ấn nút **Delete**.
- Nhập **book-image-resize-stores-by-myself** và ấn **Delete bucket**.
- Chọn bucket **book-image-stores-by-myself**.
- Ấn nút **Delete**.
- Nhập **book-image-stores-by-myself** và ấn **Delete bucket**
- Chọn bucket **fcj-book-shop-by-myself**.
- Ấn nút **Delete**.
- Nhập **fcj-book-shop-by-myself** và ấn **Delete bucket**.

3. Xoá REST API
- Mở bảng điều khiển của [API Gateway](https://ap-southeast-2.console.aws.amazon.com/apigateway/main/apis?region=ap-southeast-2#).
- Chọn **fcj-serverless-api**.
- Ấn **Delete**.
- Nhập **confirm** và ấn **Delete**.

4. Xoá Lambda function
- Mở bảng điều khiển của [AWS Lambda](https://ap-southeast-2.console.aws.amazon.com/lambda/home?region=ap-southeast-2#/functions).
- Chọn **book_create** function
- Ấn **Actions**.
- Chọn **Delete**.
- Nhập **delete** và ấn **Delete**.
- Tương tự với **resize_image**, **books_list**, **book_create**, **book_delete** function.
