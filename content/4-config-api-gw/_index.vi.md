---
title : "Cấu hình API Gateway"
date :  "`r Sys.Date()`" 
weight : 4
chapter : false
pre : " <b> 4. </b> "
---

Tiếp theo, chúng ta sẽ thiết lập API Gateway để tương tác với các hàm Lambda đã tạo ở phần trước:

1. Mở [API Gateway console](https://us-east-1.console.aws.amazon.com/apigateway/main/apis?region=us-east-1).
    ![CreateRestAPI](/images/temp/1/50.png?width=90pc)

2. Cuộn xuống và nhấp vào **Build** của mục **REST API**.
    ![CreateRestAPI](/images/temp/1/51.png?width=90pc)

3. Tại trang **Create REST API**.
    - Chọn **New API** để tạo một API mới.
    - Nhập tên REST API, ví dụ: `fcj-serverless-api`.
    - Đối với **API endpoint type**, chọn **Regional**.
    - Nhấp vào **Create API**.
      ![CreateRestAPI](/images/temp/1/52.png?width=90pc)

4. Tại trang **Resources - fcj-serverless-api**.
    - Nhấp vào **Create resource**.
      ![CreateRestAPI](/images/temp/1/53.png?width=90pc)

5. Tại trang **Create resource**.
    - Nhập tên resource, ví dụ: **books**.
    - Sau đó nhấp vào **Create Resource**.
      ![CreateRestAPI](/images/temp/1/54.png?width=90pc)

Vậy là chúng ta đã tạo một REST API mới và resource cho nó. Tiếp theo, chúng ta sẽ tạo các phương thức để tương tác với các hàm Lambda và thiết lập chúng.

1. [Tạo phương thức](4-1-create-methods/)
2. [Thiết lập và kích hoạt CORS](4-2-setting-and-cors/)
