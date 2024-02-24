# HSRP kết hợp với Spanning-tree Protocol

## Tìm hiểu khái niệm

- Kết hợp Hot Standby Router Protocol (HSRP) với Spanning Tree Protocol (STP) là một phần quan trọng của thiết kế mạng để cung cấp sự tin cậy và sự dự phòng trong mạng LAN. Dưới đây là cách kết hợp HSRP với STP:

	- `Thiết lập HSRP trên các Router`: Đầu tiên, bạn cần thiết lập HSRP trên các router trong mạng LAN của bạn. HSRP cho phép bạn tạo ra một IP gateway ảo được chia sẻ giữa các router trong cùng một HSRP group. Một trong số các router sẽ đóng vai trò là Active router và các router khác sẽ đóng vai trò là Standby router.

	- `Thiết lập STP trên Switches`: Tiếp theo, bạn cần thiết lập STP trên các switch trong mạng LAN của bạn. STP giúp ngăn chặn và quản lý các vòng lặp trong mạng LAN bằng cách chọn ra một đường đi duy nhất từ mỗi switch tới root bridge.

	- `Kết hợp HSRP với STP`: Trong một mạng được thiết kế tốt, bạn nên đặt gateway HSRP trên một VLAN và cấu hình STP trên VLAN đó. Điều này đảm bảo rằng chỉ có một router Active trong HSRP group và một đường đi duy nhất từ switch tới router Active, giảm thiểu rủi ro về loop và tăng tính sẵn sàng của mạng.

	- `Kiểm tra và Xác nhận`: Sau khi thiết lập, hãy kiểm tra kết nối giữa HSRP và STP để đảm bảo rằng mạng của bạn hoạt động như mong đợi và rằng bạn đã loại bỏ hoặc giảm thiểu vòng lặp trong mạng LAN.

- Kết hợp HSRP với STP giúp tăng tính sẵn sàng và độ tin cậy của mạng LAN bằng cách cung cấp sự dự phòng cho cả lớp 3 (HSRP) và lớp 2 (STP). Điều này làm giảm thiểu rủi ro về sự cố và đảm bảo rằng mạng của bạn có thể hoạt động liên tục và không bị gián đoạn.

## Cấu hình kết hợp

- Cấu hình kết hợp HSRP với STP trên một mạng LAN đơn giản sử dụng thiết bị Cisco.

- Giả sử bạn có một mạng LAN với 2 router và 2 switch, và bạn muốn kết hợp HSRP với STP để cung cấp sự dự phòng và ngăn chặn các vòng lặp. Router sẽ thực hiện chức năng HSRP, trong khi Switch sẽ thực hiện chức năng STP.

1. Cấu hình HSRP trên Router 1 và Router 2

```sh
Router1(config)# interface GigabitEthernet0/0
Router1(config-if)# ip address 192.168.1.1 255.255.255.0
Router1(config-if)# standby 1 ip 192.168.1.254
Router1(config-if)# standby 1 priority 110
Router1(config-if)# standby 1 preempt
Router1(config-if)# exit

Router2(config)# interface GigabitEthernet0/0
Router2(config-if)# ip address 192.168.1.2 255.255.255.0
Router2(config-if)# standby 1 ip 192.168.1.254
Router2(config-if)# standby 1 priority 100
Router2(config-if)# standby 1 preempt
Router2(config-if)# exit
```
==> Trong đoạn mã trên, chúng ta đã thiết lập HSRP trên cổng `GigabitEthernet0/0` của cả hai router. Router 1 có priority cao hơn (110) so với Router 2 (100), do đó sẽ trở thành Active router khi mạng hoạt động bình thường.

2. Cấu hình STP trên Switch 1 và Switch 2

```sh
Switch1(config)# spanning-tree mode pvst
Switch1(config)# interface range GigabitEthernet0/1 - 2
Switch1(config-if-range)# spanning-tree portfast
Switch1(config-if-range)# exit

Switch2(config)# spanning-tree mode pvst
Switch2(config)# interface range GigabitEthernet0/1 - 2
Switch2(config-if-range)# spanning-tree portfast
Switch2(config-if-range)# exit
```

==> Trong đoạn mã trên, chúng ta đã thiết lập STP (pvst) trên cả hai switch và kích hoạt PortFast trên các cổng kết nối với thiết bị cuối (như máy tính hoặc server).

## Kiểm tra cấu hình

1. Kiểm tra cấu hình HSRP trên Router

```sh
Router1# show standby
Router1# show standby brief
```

2. Kiểm tra cấu hình STP trên Switch

```sh
Switch1# show spanning-tree
```