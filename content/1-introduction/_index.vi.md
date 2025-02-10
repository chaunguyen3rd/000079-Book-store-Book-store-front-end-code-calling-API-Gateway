---
title : "Giới thiệu API Gateway / DynamoDB"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 1. </b> "
---
#### Tổng quan

#### Giới thiệu API Gateway

Amazon API Gateway là dịch vụ được quản lý hoàn toàn giúp các nhà phát triển dễ dàng tạo, phát hành, duy trì, giám sát và bảo vệ API ở mọi quy mô. API đóng vai trò là "cửa trước" cho các ứng dụng để truy cập dữ liệu, logic nghiệp vụ hoặc chức năng từ các dịch vụ backend của bạn. Bằng cách sử dụng API Gateway, bạn có thể tạo các API RESTful và API WebSocket để kích hoạt các ứng dụng giao tiếp hai chiều theo thời gian thực. API Gateway hỗ trợ các khối lượng công việc có trong container và serverless, cũng như các ứng dụng web.

API Gateway xử lý tất cả các tác vụ liên quan đến tiếp nhận và xử lý lên đến hàng trăm nghìn lệnh gọi API đồng thời, bao gồm quản lý lưu lượng truy cập, hỗ trợ CORS, xác thực và kiểm soát truy cập, điều tiết, giám sát và quản lý phiên bản API. API Gateway không yêu cầu phí tối thiểu hoặc phí ban đầu. Bạn trả tiền cho các lệnh gọi API bạn nhận được cũng như lượng dữ liệu được truyền đi và, với mô hình định giá theo bậc của API Gateway, bạn có thể giảm chi phí khi thay đổi quy mô sử dụng API.

#### Loại API

##### API RESTful

Xây dựng các API RESTful được tối ưu hóa cho khối lượng công việc serverless và backend HTTP bằng API HTTP. API HTTP là lựa chọn tốt nhất để xây dựng những API chỉ yêu cầu chức năng proxy API. Nếu API của bạn yêu cầu cả chức năng proxy API lẫn tính năng quản lý API trong cùng một giải pháp thì API Gateway cũng cung cấp cả API REST.

##### API WEBSOCKET

Xây dựng các ứng dụng giao tiếp hai chiều theo thời gian thực, chẳng hạn như ứng dụng trò chuyện và bảng điều khiển truyền phát bằng API WebSocket. API Gateway duy trì kết nối lâu dài để xử lý quá trình truyền tin nhắn giữa dịch vụ backend và máy khách của bạn.

#### API Gateway hoạt động như thế nào?

![CreateRestAPI](/images/1-introduction/New-API-GW-Diagram.png?featherlight=false&width=90pc)

#### Giới thiệu DynamoDB

Bạn tham khảo thêm về workshop DynamoDB

- [DynamoDB cơ bản](https://000060.awsstudygroup.com/vi/)
- [DynamoDB nâng cao](https://000039.awsstudygroup.com/vi/)
