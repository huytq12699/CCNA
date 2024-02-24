# Virtual Router Redundancy Protocol (VRRP)

## Tìm hiểu chung

1. Khái niệm

- `VRRP (Virtual Router Redundancy Protocol)` là một giao thức mạng được sử dụng để cung cấp sự dự phòng cho các thiết bị định tuyến (router) trong mạng máy tính. 

- Giao thức này cho phép nhiều thiết bị định tuyến hoạt động cùng một lúc như một nhóm duy nhất, được biết đến là một "Virtual Router" (Định tuyến ảo). Một trong số các thiết bị trong nhóm sẽ giữ vai trò chính là `Router Master`, trong khi các thiết bị khác trong nhóm sẽ là `Router Backup`.

- Khi Router Master gặp sự cố (như mất kết nối hoặc lỗi phần cứng), một trong số các Router Backup sẽ tự động trở thành Router Master mới, đảm bảo rằng mạng vẫn hoạt động mà không có thời gian chết (downtime). Quá trình này được thực hiện một cách tự động và trong thời gian rất ngắn, thường chỉ trong vài giây.

2. Cách hoạt động

- Cơ chế hoạt động cơ bản của VRRP là các thiết bị trong nhóm sẽ liên tục trao đổi các thông điệp `hello` để theo dõi trạng thái của nhau.

- Router Master sẽ gửi các gói `hello` tới các Router Backup để thông báo rằng nó vẫn hoạt động.

- Nếu một `Router Backup` không nhận được bất kỳ gói `hello` nào từ `Router Master` trong một khoảng thời gian nhất định, nó sẽ giả định rằng Router Master đã gặp sự cố và sẵn sàng tiếp nhận gói tin từ mạng.

==> VRRP thường được sử dụng trong các mạng LAN (Local Area Network) để cung cấp sự tin cậy và sự liên tục vận hành cho các kết nối mạng quan trọng như truy cập Internet hoặc các dịch vụ mạng nội bộ.

## Cấu hình

### VRRP version 2

1. Router đóng vai trò `Master`

```sh
interface <interface_name>
 ip address <IP_cong> <subnet_mask>
 standby <VRRP_group> <IP_virtual_router>
 standby <VRRP_group> priority <value>
```

2. Router đóng vai trò `Backup`

```sh
interface <interface_name>
 ip address <IP_cong> <subnet_mask>
 standby <VRRP_group> <IP_virtual_router>
 standby <VRRP_group> preempt
```

### VRRP version 3

1. Router đóng vai trò `Master`

```sh
interface <interface_name>
 ip address <IP_cong> <subnet_mask>
 vrrp <VRRP_group> <IP_virtual_router>
 vrrp <VRRP_group> priority <value>
```

2. Router đóng vai trò `Backup`

```sh
interface <interface_name>
 ip address <IP_cong> <subnet_mask>
 vrrp <VRRP_group> <IP_virtual_router>
 vrrp <VRRP_group> preempt
```

### Ví dụ cụ thể

- Cấu hình VRRP trên 2 router Cisco. Trong đó:

	+ `Router1` là `Master`

	+ `Router2` là `Backup` 

	+ Chúng ta sẽ sử dụng địa chỉ IP `192.168.1.1` cho Virtual Router.

	+ Sử dụng VRRP `version 3`.

1. Router1 (Master)

```sh
interface GigabitEthernet0/0
 ip address 192.168.1.2 255.255.255.0
 vrrp 1 ip 192.168.1.1
 vrrp 1 priority 150
```

- Trong cấu hình này:

	+ Router1 có địa chỉ IP là `192.168.1.2/24` trên interface `GigabitEthernet0/0`.

	+ VRRP group là `1`.

	+ Địa chỉ IP của Virtual Router là `192.168.1.1`.

	+ Priority của Router1 là `150`, cao hơn so với Router2, vì vậy Router1 sẽ là Master.

2. Router2 (Backup)

```sh
interface GigabitEthernet0/0
 ip address 192.168.1.3 255.255.255.0
 vrrp 1 ip 192.168.1.1
 vrrp 1 preempt
```

- Trong đó:

	+ Router2 có địa chỉ IP là `192.168.1.3/24` trên interface `GigabitEthernet0/0`.

	+ VRRP group là `1`.

	+ Địa chỉ IP của Virtual Router là `192.168.1.1`.

3. Lưu ý

- Khi cấu hình cần đảm bảo rằng các thiết lập trên cả hai router đều giống nhau, bao gồm IP, VRRP group và key-string để đảm bảo tính toàn vẹn của kết nối. Nếu có bất kỳ thay đổi nào, hệ thống sẽ không hoạt động đúng cách.

## Kiểm tra cấu hình

1. Hiển thị cấu hình VRRP

```sh
show vrrp
```
2. Hiển thị thông tin chi tiết về một nhóm VRRP cụ thể

```sh
show vrrp [interface interface_name] [group group_number]
```

3. Hiển thị thông tin chi tiết về tất cả các nhóm VRRP trên một giao diện cụ thể

```sh
show vrrp interface [interface_name]
```

4. Hiển thị thông tin chi tiết về tất cả các nhóm VRRP trên toàn bộ router

```sh
show vrrp detail
```

5. Kiểm tra trạng thái của Virtual Router

```sh
show vrrp brief
```

6. Kiểm tra xem router đang hoạt động với vai trò Master hay Backup

```sh
show vrrp [interface interface_name] [group group_number] detail
```