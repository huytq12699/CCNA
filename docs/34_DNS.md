# Domain Name Server (DNS)

## Tìm hiểu các khái niệm

- DNS (Domain Name System) là một hệ thống phân giải tên miền dùng để chuyển đổi tên miền dễ đọc thành địa chỉ IP của máy chủ. DNS giúp cho việc giao tiếp và truy cập Internet trở nên dễ dàng hơn đối với con người bằng cách sử dụng tên miền thay vì phải ghi nhớ các địa chỉ IP phức tạp.

- `Tên miền (Domain Name)`: Đây là tên định danh dễ đọc được sử dụng để xác định các tài nguyên trên Internet. Ví dụ: google.com, facebook.com.

- `Địa chỉ IP (IP Address)`: Đây là định danh số duy nhất của một máy chủ hoặc thiết bị trên Internet. Ví dụ: địa chỉ IP của Google có thể là 172.217.12.206.

- `DNS Server`: Là các máy chủ chạy phần mềm DNS, chịu trách nhiệm giữa việc phân giải tên miền thành địa chỉ IP và cung cấp thông tin về tên miền khi được yêu cầu.

- `Record DNS`: Là các bản ghi dữ liệu trong cơ sở dữ liệu DNS, chứa thông tin về tên miền và địa chỉ IP tương ứng. Các loại bản ghi DNS bao gồm:

	+ `A Record`: Liên kết một tên miền với một địa chỉ IPv4.

	+ `AAAA Record`: Liên kết một tên miền với một địa chỉ IPv6.

	+ `CNAME Record`: Liên kết một tên miền với một tên miền khác.

	+ `MX Record`: Xác định máy chủ thư điện tử cho một tên miền.

## Cách hoạt động

- Cách hoạt động cơ bản của hệ thống DNS (Domain Name System) là quá trình chuyển đổi tên miền (domain names) thành địa chỉ IP (IP addresses) và ngược lại.

1. `Yêu cầu phân giải DNS (DNS Resolution Request)`: Khi bạn nhập một tên miền vào trình duyệt web hoặc ứng dụng, thiết bị của bạn gửi một yêu cầu phân giải DNS đến máy chủ DNS.

2. `Truy vấn máy chủ DNS (DNS Server Query)`: Thiết bị của bạn gửi yêu cầu phân giải DNS đến máy chủ DNS được cấu hình trong cài đặt mạng hoặc máy chủ DNS của nhà cung cấp dịch vụ Internet.

3. `Tra cứu bản ghi DNS (DNS Record Lookup)`: Máy chủ DNS nhận được yêu cầu và kiểm tra trong cơ sở dữ liệu của mình để tìm kiếm thông tin về tên miền được yêu cầu. Thông tin này có thể được lưu trữ trên máy chủ DNS đó hoặc được lấy từ các máy chủ DNS khác trong mạng.

4. `Trả lời DNS (DNS Response)`: Máy chủ DNS trả về địa chỉ IP tương ứng với tên miền được yêu cầu trong phản hồi DNS. Nếu không tìm thấy tên miền trong cơ sở dữ liệu của mình, máy chủ DNS có thể chuyển tiếp yêu cầu đến các máy chủ DNS khác.

5. `Cập nhật bản ghi DNS (DNS Record Update)`: Thông tin trả về từ máy chủ DNS có thể được lưu trữ tạm thời trên thiết bị của bạn để tăng tốc độ truy cập trong tương lai. Nếu thông tin đã lỗi thời hoặc thay đổi, máy chủ DNS sẽ cập nhật cơ sở dữ liệu của mình để phản ánh những thay đổi đó.

6. `Truy cập tài nguyên (Accessing Resources)`: Sau khi nhận được địa chỉ IP, thiết bị của bạn sẽ sử dụng nó để truy cập tài nguyên trên Internet hoặc trong mạng nội bộ.