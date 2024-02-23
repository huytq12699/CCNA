# Routing inter-VLAN trên SW Layer 3

## Tìm hiểu chung

- `Routing inter-VLAN` (Routing giữa các VLAN) là quá trình định tuyến gói dữ liệu giữa các mạng con ảo LAN (VLANs) khác nhau trên cùng một hệ thống mạng. VLANs là các phân đoạn logic của mạng vật lý, cho phép chia một mạng vật lý thành nhiều mạng nhỏ hơn, cách ly với nhau về mặt broadcast và truy cập. Tuy nhiên, trong một môi trường mạng, có thể cần thiết lập giao tiếp giữa các VLAN để cho phép các thiết bị trong các VLAN khác nhau giao tiếp với nhau.

- Routing inter-VLAN có thể được thực hiện bằng cách sử dụng một router hoặc một switch Layer 3. Ở bài này ta sẽ tìm hiểu cách thực hiện trên Switch Layer 3.

- Trên Switch Layer 3: Switch được cấu hình để thực hiện chức năng định tuyến giữa các VLAN thông qua các SVI (Switched Virtual Interfaces) hoặc cổng Layer 3.

- Các lợi ích của routing inter-VLAN bao gồm:

	+ `Cách ly Traffic`: Giúp cách ly lưu lượng mạng giữa các phần khác nhau của mạng, cải thiện hiệu suất và bảo mật.

	+ `Tăng linh hoạt`: Cho phép tổ chức mạng linh hoạt hơn bằng cách cho phép giao tiếp giữa các nhóm thiết bị khác nhau dù chúng được phân tách vào các VLAN riêng biệt.

	+ `Optimize Performance`: Cho phép bạn tối ưu hóa hiệu suất mạng bằng cách định tuyến dữ liệu trực tiếp giữa các VLAN thay vì phải chuyển tiếp dữ liệu qua router bên ngoài.

## Cách cấu hình

### Các bước cấu hình

1. `Tạo VLAN`: Bạn cần tạo các VLAN trên switch của mình. Mỗi VLAN đại diện cho một miền broadcast riêng biệt. Gán cổng cho các VLAN tùy theo thiết kế mạng của bạn.

2. `Tạo Inter-VLAN Routing Interface (SVI)`: Trên switch Layer 3, bạn cần tạo một giao diện ảo (SVI - Switched Virtual Interface) cho mỗi VLAN. Giao diện này sẽ hoạt động như cổng gateway cho các thiết bị trong VLAN đó. Gán một địa chỉ IP cho mỗi SVI.

3. `Bật tính năng Routing`: Đảm bảo rằng tính năng routing được bật trên switch của bạn. Điều này cho phép switch định tuyến gói tin giữa các VLAN.

4. `Cấu hình Chính sách Routing`: Bạn có thể cần thiết lập các Access Control Lists (ACL) hoặc các chính sách routing khác để kiểm soát luồng traffic giữa các VLAN. Điều này có thể bao gồm cho phép hoặc từ chối các loại traffic cụ thể.

5. `Cấu hình Cổng Trunk`: Các cổng trunk được sử dụng để truyền traffic cho nhiều VLAN giữa các switch. Đảm bảo các cổng trunk của bạn được cấu hình đúng để truyền traffic cho tất cả các VLAN cần được định tuyến.


### Lệnh cấu hình 

1. Trên SW Layer 2: 

- Tạo Vlan và gán cổng vào các Vlan tương ứng

```sh
Switch-L2(config)# vlan 10
Switch-L2(config-vlan)# name Sales

Switch-L2(config)# vlan 20
Switch-L2(config-vlan)# name Marketing

Switch-L2(config)# interface range gigabitEthernet 0/2 - 4
Switch-L2(config-if-range)# no shut
Switch-L2(config-if-range)# switchport mode access
Switch-L2(config-if-range)# switchport access vlan 10

Switch-L2(config)# interface range gigabitEthernet 0/5 - 7
Switch-L2(config-if-range)# no shut
Switch-L2(config-if-range)# switchport mode access
Switch-L2(config-if-range)# switchport access vlan 20
```

- Cấu hình cổng trunk: Cấu hình một cổng trên Switch Layer 2 để làm cổng trunk và chuyển giao traffic của tất cả các VLAN tới Switch Layer 3

```sh
Switch-L2(config)# interface gigabitEthernet 0/1
Switch-L2(config-if)# no shut
Switch-L2(config-if)# switchport mode trunk
```

2. Trên SW Layer 3:

- Tạo VLAN và SVI (Switched Virtual Interface): Tạo các VLAN trên switch Layer 3 và tạo SVI cho mỗi VLAN.

```sh
Switch-L3(config)# vlan 10
Switch-L3(config-vlan)# name Sales

Switch-L3(config)# vlan 20
Switch-L3(config-vlan)# name Marketing

Switch-L3(config)# interface vlan 10
Switch-L3(config-if)# ip address 192.168.10.1 255.255.255.0
Switch-L3(config-if)# no shut

Switch-L3(config)# interface vlan 20
Switch-L3(config-if)# ip address 192.168.20.1 255.255.255.0
Switch-L3(config-if)# no shut
```

3. Kích hoạt tính năng định tuyến và kích hoạt định tuyến inter-VLAN trên Switch Layer 3

```sh
Switch-L3(config)# ip routing
```

4. Kích hoạt định tuyến trên switch Layer 2: Cấu hình switch Layer 2 để chuyển hướng traffic inter-VLAN tới switch Layer 3.

```sh
Switch-L2(config)# ip default-gateway 192.168.10.1
```

## Kiểm tra cấu hình

1. Trên SW layer 2

- Kiểm tra cấu hình VLAN:

```sh
Switch-L2# show vlan
```

- Kiểm tra cấu hình cổng:

```sh
Switch-L2# show interface status
```


- Kiểm tra cấu hình cổng trunk:

```sh
Switch-L2# show interfaces trunk
```


2. Trên SW layer 3

- Kiểm tra cấu hình VLAN và SVI:

```sh
Switch-L3# show vlan
Switch-L3# show ip interface brief
```


- Kiểm tra bảng định tuyến:

```sh
Switch-L3# show ip route
```


- Kiểm tra cấu hình định tuyến:

```sh
Switch-L3# show ip protocols
```


- Kiểm tra trạng thái kết nối:

```sh
Switch-L3# show cdp neighbors
```
