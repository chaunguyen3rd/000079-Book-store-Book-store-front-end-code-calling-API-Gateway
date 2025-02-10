---
title : "Kiểm tra API bằng Postman"
date :  "`r Sys.Date()`" 
weight : 5
chapter : false
pre : " <b> 5. </b> "
---
Trong bước này, chúng ta sẽ kiểm tra hoạt động của các API bằng công cụ [Postman](https://www.postman.com/downloads/).

#### Kiểm tra API liệt kê

1. Nhấp vào **+** để thêm một tab mới.
    - Chọn phương thức **GET**.
    - Nhập URL của API liệt kê đã ghi lại từ bước trước.
    - Nhấp vào **Send**.
      ![TestListAPI](/images/temp/1/77.png?width=90pc)
Kết quả trả về là toàn bộ dữ liệu của bảng **Books** đã được xử lý.

#### Kiểm tra API ghi

1. Tương tự, tạo một tab mới.
    - Chọn phương thức **POST**.
    - Nhập URL của API ghi đã ghi lại từ bước trước.
    - Chọn **Body**.
    - Chọn **form-data**.
    - Điền **Key** và **Value** như dưới đây. Thay đổi loại của Key **image** thành **File** như hình dưới. Và với Value của Key **image**, chọn đường dẫn tệp cục bộ của bạn.
      - id: `5`
      - name: `Amazon Web Services in Action 2nd Edition`
      - author: `Andreas Wittig`
      - price: `59.99`
      - category: `IT`
      - description: `Amazon Web Services in Action, Second Edition is a comprehensive introduction to computing, storing, and networking in the AWS cloud. You'll find clear, relevant coverage of all the essential AWS services you to know, emphasizing best practices for security, high availability and scalability`
      - image: aws-logo.png
    - Nhấp vào **Send**. Chờ một lúc, xem kết quả trả về **Successfully created item**.
      ![TestListAPI](/images/temp/1/78.png?width=90pc)

2. Mở bảng **Books** trong DynamoDB console để kiểm tra dữ liệu.
    - Trước khi gọi API ghi.
      ![TestListAPI](/images/temp/1/79.png?width=90pc)
    - Sau khi gọi API ghi.
      ![TestListAPI](/images/temp/1/80.png?width=90pc)

#### Kiểm tra API xóa

1. Tương tự, tạo một tab mới.
    - Chọn phương thức **DELETE**.
    - Nhập URL của API ghi đã ghi lại từ bước trước. Thay đổi **{id}** thành book_id bạn muốn xóa, ví dụ **5**.
    - Nhấp vào **Send**. Chờ một lúc, xem kết quả trả về **Successfully delete item!**.
      ![TestListAPI](/images/temp/1/81.png?width=90pc)

2. Mở bảng **Books** trong DynamoDB console để kiểm tra dữ liệu.
    ![TestListAPI](/images/temp/1/79.png?width=90pc)

3. Mở bucket **book-image-resize-stores-by-myself** để kiểm tra đối tượng. Tệp **aws-logo.jpg** đã bị xóa.
    ![TestListAPI](/images/temp/1/82.png?width=90pc)
