# DHCP relay

## Tìm hiểu chung

1. Khái niệm

- `DHCP Relay` là một tính năng hoặc dịch vụ trong mạng máy tính được sử dụng để chuyển tiếp các yêu cầu DHCP từ các mạng con không có máy chủ DHCP đến máy chủ DHCP trên mạng cục bộ hoặc mạng chính. Điều này cho phép máy chủ DHCP cung cấp địa chỉ IP và các thông tin cấu hình mạng khác cho các thiết bị trong các mạng con.

2. Tại sao cần sử dụng DHCP Relay?

- `Mạng lớn và phân tán`: Trong mạng lớn với nhiều VLAN hoặc mạng con, việc triển khai máy chủ DHCP trên mỗi VLAN có thể không hiệu quả và gây lãng phí. DHCP Relay cho phép một máy chủ DHCP trên mạng chính phục vụ các mạng con khác.

- `Quản lý trung tâm`: Sử dụng một máy chủ DHCP trung tâm giúp quản lý dễ dàng hơn và giảm sự phức tạp của việc cấu hình và duy trì nhiều máy chủ DHCP trên mạng.

## Cách hoạt động

1. `Thiết bị DHCP Relay`: Thiết bị như router hoặc layer 3 switch được cấu hình để làm DHCP Relay Agent.

2. `Chuyển tiếp yêu cầu DHCP`: Khi một thiết bị trên mạng con gửi yêu cầu DHCP, DHCP Relay Agent nhận yêu cầu này và chuyển tiếp nó đến máy chủ DHCP.

3. `Thêm thông tin cần thiết`: DHCP Relay Agent thêm thông tin về giao diện mạng của nó vào yêu cầu DHCP trước khi chuyển tiếp nó. Thông tin này giúp máy chủ DHCP xác định subnet mà yêu cầu DHCP được gửi từ.

4. `Phản hồi DHCP`: Máy chủ DHCP phản hồi với địa chỉ IP và thông tin cấu hình mạng khác dựa trên yêu cầu DHCP và thông tin mạng từ DHCP Relay Agent.

5. `Chuyển tiếp phản hồi DHCP`: DHCP Relay Agent nhận phản hồi DHCP và chuyển tiếp nó đến thiết bị mà yêu cầu DHCP đã được gửi từ.