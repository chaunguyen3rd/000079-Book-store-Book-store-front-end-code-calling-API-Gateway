---
title : "Thiết lập API Gateway"
date :  "`r Sys.Date()`" 
weight : 4
chapter : false
pre : " <b> 4. </b> "
---
Tiếp theo, chúng ta sẽ thiết lập API Gateway tương tác với các Lambda function đã tạo ở phần trước:

1. Mở bảng điều khiển [API Gateway console](https://ap-southeast-2.console.aws.amazon.com/apigateway/main/apis?region=ap-southeast-2).
![CreateRestAPI](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/50.png?width=90pc)

2. Kéo xuống và bấm vào **Build** ở **REST API**.
![CreateRestAPI](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/51.png?width=90pc)

3. Ở trang **Create REST API**.
    - Chọn **New API** để tạo ra một API mới.
    - Nhập tên REST API, ví dụ: **fcj-serverless-api**.
    - Đối với **API endpoint type**, chọn **Regional**.
    - Nhấn nút **Create API**.
![CreateRestAPI](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/52.png?width=90pc)

4. Ở trang **Resources - fcj-serverless-api**.
    - Nhấn nút **Create resource**.
![CreateRestAPI](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/53.png?width=90pc)

5. Ở trang **Create resource**.
    - Nhập tên resource, ví dụ: **books**.
    - Sau đó nhấn nút **Create Resource**.
![CreateRestAPI](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/54.png?width=90pc)

Vậy là chúng ta đã tạo xong một REST API mới và resource cho nó. Tiếp theo chúng ta sẽ tạo các method tương tác với Lambda function và cái đặt chúng:
1. [Tạo các method](4-1-create-methods/)
2. [Cài đặt và kích hoạt CORS](4-2-setting-and-cors/)

