# Network Address Translation (NAT)

## Khái niệm

- Đây là một kỹ thuật được sử dụng trong mạng máy tính để ánh xạ địa chỉ IP từ một miền mạng vào miền mạng khác. NAT thường được sử dụng trong các mạng gia đình, doanh nghiệp và cả trên Internet để cho phép nhiều thiết bị trong một mạng nội bộ chia sẻ một địa chỉ IP công cộng hoặc để kết nối mạng nội bộ với Internet thông qua một hoặc một số ít địa chỉ IP.

## Hoạt động

1. `Local Network (Mạng nội bộ)`: Một mạng nội bộ có thể chứa nhiều thiết bị, như máy tính, điện thoại thông minh, máy in, v.v. Mỗi thiết bị trong mạng này có địa chỉ IP nội bộ duy nhất, thường là địa chỉ không hợp lệ trong Internet (ví dụ: 192.168.x.x).

2. `Gateway/NAT Device (Thiết bị cổng/NAT)`: Một thiết bị trung gian, thường là router, được cấu hình với NAT. Khi các gói dữ liệu đi từ mạng nội bộ ra Internet hoặc ngược lại, NAT sẽ thực hiện chuyển đổi địa chỉ IP của các gói dữ liệu theo các quy tắc được định sẵn.

3. `Public Network (Mạng công cộng)`: Đây là mạng lớn hơn nơi mạng nội bộ được kết nối tới, thường là Internet. Một địa chỉ IP công cộng được cung cấp cho mạng nội bộ thông qua NAT.

## Phân loại

1. `Static NAT`: Một địa chỉ IP công cộng được ánh xạ một cách cố định tới một địa chỉ IP nội bộ.

2. `Dynamic NAT`: Các địa chỉ IP nội bộ được ánh xạ động lên các địa chỉ IP công cộng trong một bộ phận của pool địa chỉ IP công cộng.

3. `NAT Overload (PAT - Port Address Translation)`: Loại NAT này sử dụng một địa chỉ IP công cộng và số cổng để ánh xạ các địa chỉ IP nội bộ và cổng tới Internet. Đây là loại NAT phổ biến nhất và cho phép nhiều thiết bị trong mạng nội bộ chia sẻ một địa chỉ IP công cộng duy nhất.

## Cấu hình NAT

1. Static NAT

-  Lệnh cấu hình

```sh
Router(config)#ip nat inside source static [inside local address] [inside global address]
```

-  Sau khi cấu hình xong phải áp dụng vào cổng in và cổng out.

```sh
Router(config)#interface <interface>
Router(config-if)#ip nat inside

Router(config)#interface <interface> 
Router(config-if)#ip nat outside 
```

- Ví dụ: Cấu hình một máy chủ web trong mạng nội bộ có địa chỉ IP nội bộ là 192.168.1.10 được ánh xạ tới địa chỉ IP công cộng là 203.0.113.10.

```sh
interface GigabitEthernet0/0
 ip address 203.0.113.1 255.255.255.0
 ip nat outside

interface GigabitEthernet0/1
 ip address 192.168.1.1 255.255.255.0
 ip nat inside

ip nat inside source static 192.168.1.10 203.0.113.10

```

2. Dynamic NAT

- Lệnh cấu hình:

```sh
			Router(config)#ip nat pool [tên pool] [ip global inside] [subnet mask] 
			Router(config)#ip nat inside source list [tên số hiệu ACL] pool [tên pool] overload 
			Router(config)#access-list [số hiệu] permit [địa chỉ] [windcard mask] 
```

- VD:

```sh
			R(config)#access-list 2 permit 10.0.0.0 0.0.0.255 
			R(config)#ip nat pool nat-pool2 179.9.8.20 255.255.255.240 
			R(config)#ip nat inside source list 2 nat-pool2 overload 
```

3. NAT overload

- Lệnh cấu hình

```sh
			Router(config)#ip nat inside source list [tên số hiệu ACL] interface [cổng ra] overload 
			Router(config)#access-list [số hiệu] permit [địa chỉ] [windcard mask]
```
- VD:

```sh
			interface G0/0
 			  ip address 203.0.113.1 255.255.255.0
 			  ip nat outside

			interface G0/1
 			  ip address 192.168.1.1 255.255.255.0
 			  ip nat inside

			ip nat inside source list 1 interface G0/0 overload

			access-list 1 permit 192.168.1.0 0.0.0.255
```
4. Xóa NAT

- Lệnh xóa tất cả Dynamic Nat trên toàn bộ các interface

```sh
Router#clear ip nat translation
```
- Lệnh xóa các Single Nat trên từng interface

```sh
Router#clear ip nat translation [inside/outside] [global ip - local ip]
```
- Lệnh xóa các Extended Nat trên từng interface

```sh
Router#clear ip nat translation protocol [inside/outside] [global ip - global port – local ip – local port] 
```

## Lệnh kiểm tra cấu hình

1. Kiểm tra trạng thái NAT trên router

```sh
show ip nat translations
```
2. Kiểm tra cấu hình NAT trên router

```sh
show running-config | include ip nat
```

3. Kiểm tra số lượng kết nối NAT trong bảng NAT

```sh
show ip nat statistics
```

4. Kiểm tra NAT Pool (đối với Dynamic NAT)

```sh
show ip nat pool
```