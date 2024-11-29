---
title : "Thiết lập API Gateway"
date :  "`r Sys.Date()`" 
weight : 4
chapter : false
pre : " <b> 4. </b> "
---
Tiếp theo, chúng ta sẽ thiết lập API Gateway tương tác với các Lambda function đã tạo ở phần trước:
1. Mở bảng điều khiển của [API Gateway](https://ap-southeast-2.console.aws.amazon.com/apigateway/main/apis?region=ap-southeast-2)
![CreateRestAPI](/images/1/39.png?width=90pc)
2. Kéo xuống và ấn nút **Build** của mục **REST API**
![CreateRestAPI](/images/1/40.png?width=90pc)

4. Chọn **REST** cho **Protocol**
- Chọn **New API** để tạo một API mới
- Nhập tên cho REST API, ví dụ: **fcj-serverless-api**
- Tại mục **API enpoint type**: chọn **Regional**
- Ấn nút **Create API**
![CreateRestAPI](/images/1/41.png?width=90pc)

5. Ấn vào API vừa tạo xong, sau đó chọn **Create resource**
![CreateRestAPI](/images/1/42.png?width=90pc)

6. Ấn nút **Actions**, sau đó chọn **Create resource**

![CreateRestAPI](/images/4-config-api-gw/4-config-api-gw-6.png?featherlight=false&width=90pc)

7. Nhập tên cho resource, ví dụ: **books**
- Sau đó ấn nút **Create Resource**
![CreateRestAPI](/images/1/43.png?width=90pc)

Vậy là chúng ta đã tạo xong một REST API mới và resource cho nó. Tiếp theo chúng ta sẽ tạo các method tương tác với Lambda function và cái đặt chúng:
1. [Tạo các method](4-1-create-methods/)
2. [Cài đặt và kích hoạt CORS](4-2-setting-and-cors/)

