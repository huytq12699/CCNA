# So sánh Router & Switch

1. Mục đích:

- Router: Router được sử dụng để kết nối các mạng khác nhau với nhau, quyết định tuyến đường cho gói dữ liệu và thực hiện các chức năng điều khiển truy cập mạng như NAT và bảo mật.

- Switch: Switch được sử dụng để kết nối các thiết bị mạng trong một mạng cục bộ (LAN), chuyển tiếp dữ liệu giữa các thiết bị mạng dựa trên địa chỉ MAC và loại bỏ xung đột dữ liệu.

2. Chuyển tiếp dữ liệu:

- Router: Router chuyển tiếp dữ liệu giữa các mạng khác nhau dựa trên địa chỉ IP, quyết định tuyến đường tốt nhất cho gói dữ liệu.

- Switch: Switch chuyển tiếp dữ liệu giữa các thiết bị trong cùng một mạng cục bộ (LAN) dựa trên địa chỉ MAC.

3. Quyết định tuyến đường:

- Router: Router quyết định tuyến đường tốt nhất cho gói dữ liệu sử dụng các thuật toán định tuyến như RIP, OSPF, hoặc BGP.

- Switch: Switch không quyết định tuyến đường, nó chỉ chuyển tiếp dữ liệu giữa các cổng dựa trên địa chỉ MAC.

4. Loại bỏ xung đột:

- Router: Router không loại bỏ xung đột dữ liệu trong mạng, vì nó thường chỉ kết nối hai hoặc nhiều mạng khác nhau.

- Switch: Switch loại bỏ xung đột dữ liệu bằng cách cung cấp băng thông riêng biệt cho mỗi cổng, không có xung đột giữa các thiết bị kết nối.

5. Bảo mật:

- Router: Router cung cấp các tính năng bảo mật như firewall, NAT, VPN, và access control để bảo vệ mạng.

- Switch: Switch cung cấp bảo mật cơ bản như VLANs và port security để ngăn chặn truy cập trái phép vào mạng.

> Tóm tắt qua bảng dưới đây

| Đặc điểm                | Router                                      | Switch                                      |
|-------------------------|---------------------------------------------|---------------------------------------------|
| Mục đích                | Kết nối các mạng khác nhau và chuyển tiếp dữ liệu giữa chúng | Kết nối các thiết bị trong cùng một mạng và chuyển tiếp dữ liệu giữa chúng |
| Chức năng chính         | Định tuyến, chuyển tiếp dữ liệu, bảo mật, quản lý mạng | Chuyển tiếp dữ liệu, loại bỏ xung đột, tích hợp mạng, tăng băng thông |
| Quản lý dải địa chỉ IP | Có thể quản lý địa chỉ IP cho mỗi giao diện mạng | Không quản lý địa chỉ IP; chỉ chuyển tiếp dữ liệu dựa trên địa chỉ MAC |
| Các giao diện           | Có nhiều giao diện mạng (Ethernet, Serial, Wi-Fi) | Có nhiều cổng Ethernet |
| Địa chỉ MAC            | Sử dụng để xác định các giao diện mạng | Sử dụng để xác định các thiết bị kết nối |
| Bảo mật                 | Cung cấp các tính năng bảo mật như ACLs, VPNs | Cung cấp tính năng bảo mật như port security, VLANs |
| Quản lý và cấu hình    | Có giao diện quản lý để cấu hình và giám sát | Có giao diện quản lý nhưng ít phức tạp hơn |
