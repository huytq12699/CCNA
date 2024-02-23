# Router-on-a-Stick

## Tìm hiểu chung

1. Khái niệm

- Router on a Stick là một kiến trúc mạng được sử dụng để kết nối các mạng VLAN (Virtual Local Area Network) với một router sử dụng một cổng duy nhất. Đây là một phương pháp hiệu quả để triển khai mạng VLAN trong các mạng nhỏ hoặc môi trường thử nghiệm.

- Cụ thể, trong một kiến trúc Router on a Stick, một router được cấu hình với một cổng được kết nối với một switch, và switch này lại kết nối với các thiết bị trên các VLAN khác nhau. Các khách hàng trong các VLAN khác nhau có thể giao tiếp qua router bằng cách sử dụng giao thức định tuyến như Router-on-a-Stick hoặc Inter-VLAN Routing.

2. Ưu điểm và nhược điểm

- Ưu điểm của Router on a Stick bao gồm:

	+ `Tiết kiệm chi phí`: Chỉ cần một cổng trên router để kết nối với switch, giảm thiểu chi phí cho việc triển khai mạng.

	+ `Quản lý dễ dàng`: Có thể quản lý và cấu hình các VLAN một cách dễ dàng tại một điểm trên router.

	+ `Linh hoạt`: Cho phép linh hoạt trong việc thêm mới hoặc thay đổi VLAN mà không cần phải thay đổi cấu hình vật lý của hệ thống.

- Bên cạnh đó còn có những nhược điểm cần xem xet khi triển khai:

	+ `Hiệu suất`: Một cổng trên router chỉ có thể xử lý một lượng lớn dữ liệu có hạn, điều này có thể gây ra hạn chế về hiệu suất nếu có lượng dữ liệu lớn đi qua.

	+ `Điểm hỏng`: Nếu cổng kết nối giữa router và switch gặp sự cố, tất cả các VLAN có thể bị ảnh hưởng.

	+ `Tăng cường lưu lượng`: Khi số lượng VLAN và lưu lượng mạng tăng, Router on a Stick có thể trở nên không đủ hiệu quả và cần phải được nâng cấp hoặc thay thế bằng các giải pháp mạng phân phối khác.

## Cách triển khai

1. `Tạo VLANs`: Xác định các VLANs bạn muốn triển khai và quyết định phân chia mạng con của mình ra làm các VLANs tương ứng.

2. `Cấu hình VLANs trên Switch`: Đặt tên và cấu hình các VLANs trên switch Layer 2. Đảm bảo rằng các cổng switch được đưa vào các VLANs chính xác.

3. `Cấu hình Trunk Port`: Cấu hình một cổng trên switch làm trunk port để kết nối với router. Trunk port cho phép chuyển giao thông từ nhiều VLANs đến router.

4. `Cấu hình Router`: Cấu hình router để tạo các subinterfaces trên cổng kết nối với switch, mỗi subinterface tương ứng với một VLAN khác nhau. Mỗi subinterface sẽ có một địa chỉ IP trong dải địa chỉ của VLAN tương ứng.

5. `Cấu hình Routing và Định tuyến`: Thiết lập phương thức định tuyến trên router để cho phép giao tiếp giữa các VLANs. Điều này có thể bao gồm cấu hình các giao thức định tuyến như RIP, OSPF hoặc cấu hình tuyến đường tĩnh.

## Cấu hình

1. Cấu hình VLANs trên Switch Cisco

```sh
Switch(config)# vlan 10
Switch(config-vlan)# name VLAN10
Switch(config)# vlan 20
Switch(config-vlan)# name VLAN20
```

2. Cấu hình Trunk Port trên Switch Cisco

```sh
Switch(config)# interface GigabitEthernet0/1
Switch(config-if)# switchport mode trunk
```

3. Cấu hình Subinterfaces trên Router Cisco

```sh
Router(config)# interface GigabitEthernet0/0
Router(config-if)# no shutdown
Router(config)# interface GigabitEthernet0/0.10
Router(config-subif)# encapsulation dot1Q 10
Router(config-subif)# ip address 192.168.10.1 255.255.255.0
Router(config)# interface GigabitEthernet0/0.20
Router(config-subif)# encapsulation dot1Q 20
Router(config-subif)# ip address 192.168.20.1 255.255.255.0
```

4. Cấu hình Định tuyến trên Router Cisco

```sh
Router(config)# ip routing
```

5. Định tuyến giữa hai VLANs trên Router Cisco

```sh
Router(config)# ip route 192.168.20.0 255.255.255.0 192.168.10.2
```

- Trong ví dụ trên

	+ VLAN10 có dải địa chỉ IP là 192.168.10.0/24.

	+ VLAN20 có dải địa chỉ IP là 192.168.20.0/24.

	+ Router sẽ có hai subinterfaces tương ứng với VLAN10 và VLAN20.

	+ Trunk port trên switch được cấu hình để chuyển giao thông từ cả hai VLANs tới router.

	+ Router được cấu hình để định tuyến giao tiếp giữa hai VLANs.

## Kiểm tra cấu hình

1. Kiểm tra cấu hình trên Router

```sh
Router# show running-config
```

2. Kiểm tra cấu hình trên Switch

```sh
Switch# show running-config
```