---
title : "Dọn dẹp"
date :  "`r Sys.Date()`" 
weight : 7
chapter : false
pre : " <b> 7. </b> "
---

1. Xóa bảng DynamoDB.
    - Mở [DynamoDB console](https://us-east-1.console.aws.amazon.com/dynamodbv2/home?region=us-east-1#dashboard).
    - Chọn **Tables** ở menu bên trái.
    - Chọn bảng **Books**.
    - Nhấp vào **Delete**.
    - Nhập `confirm` và nhấp vào **Delete**.

2. Xóa S3 bucket
    - Mở [S3 console](https://s3.console.aws.amazon.com/s3/buckets?region=us-east-1)
    - Chọn bucket **book-image-resize-stores-by-myself**.
    - Nhấp vào **Empty**.
    - Nhập `permanently delete` và nhấp vào **Empty**.
    - Chọn bucket **fcj-book-shop-by-myself**.
    - Nhấp vào **Empty**.
    - Nhập `permanently delete` và nhấp vào **Empty**.
    - Chọn bucket **book-image-resize-stores-by-myself**.
    - Nhấp vào **Delete**.
    - Nhập `book-image-resize-stores-by-myself` và nhấp vào **Delete bucket**.
    - Chọn bucket **book-image-stores-by-myself**.
    - Nhấp vào **Delete**.
    - Nhập `book-image-stores-by-myself` và nhấp vào **Delete bucket**.
    - Chọn bucket **fcj-book-shop-by-myself**.
    - Nhấp vào **Delete**.
    - Nhập `fcj-book-shop-by-myself` và nhấp vào **Delete bucket**.

3. Xóa REST API
    - Mở [API Gateway console](https://us-east-1.console.aws.amazon.com/apigateway/main/apis?region=us-east-1#)
    - Chọn **fcj-serverless-api**.
    - Nhấp vào **Delete**.
    - Nhập `confirm` và nhấp vào **Delete**.

4. Xóa các hàm Lambda
    - Mở [AWS Lambda console](https://us-east-1.console.aws.amazon.com/lambda/home?region=us-east-1#/functions)
    - Chọn hàm **book_create**.
    - Nhấp vào **Actions**.
    - Nhấp vào **Delete**.
    - Nhập `confirm` và nhấp vào **Delete**.
    - Tương tự với các hàm **resize_image**, **books_list**, **book_create**, **book_delete**.
