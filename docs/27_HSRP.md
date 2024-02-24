# Hot Standby Router Protocol (HSRP)

## Tìm hiểu chung

1. Khái niệm

- HSRP (Hot Standby Router Protocol) là một giao thức mạng được sử dụng để cung cấp tính sẵn sàng cao cho các cổng gateway mặc định trên mạng LAN. 

- HSRP cho phép bạn cấu hình hai hoặc nhiều router làm "active" và "standby", trong đó chỉ có một router active phục vụ dữ liệu trên mạng tại bất kỳ thời điểm nào. Router standby sẽ chỉ chuyển trở thành active nếu router active gặp sự cố hoặc bị ngắt kết nối.

2. Lợi ích 

- `Tăng tính sẵn sàng`: HSRP giúp tăng tính sẵn sàng của mạng bằng cách cung cấp một cổng gateway mặc định dự phòng. Nếu router active gặp sự cố, router standby sẽ chuyển trở thành active mà không gây gián đoạn đáng kể đối với các dịch vụ mạng.

- `Tăng độ tin cậy`: HSRP cung cấp một cổng gateway mặc định dự phòng, giúp giảm nguy cơ mất kết nối mạng khi router chính gặp sự cố.

- `Tăng hiệu suất`: HSRP cho phép phân phối tải mạng bằng cách chuyển giao các yêu cầu từ các thiết bị mạng đến router active hoặc standby.

## Cách hoạt động 

1. `Router Active và Router Standby`: Trong một nhóm HSRP, có hai hoặc nhiều router. Trong số này, một router được xác định là router active, và một hoặc nhiều router khác được xác định là router standby.

2. `Chia sẻ Virtual IP (VIP)`: Mỗi router trong nhóm HSRP chia sẻ cùng một địa chỉ IP ảo, được gọi là Virtual IP (VIP). VIP là địa chỉ IP mà các thiết bị trong mạng sẽ sử dụng làm cổng gateway mặc định.

3. `Router Active và Router Standby kiểm tra trạng thái`: Router active liên tục gửi các gói tin hello với thông tin HSRP đến các router standby để thông báo rằng nó vẫn hoạt động bình thường. Router standby đặt mình trong chế độ chờ và đợi thông báo này.

4. `Chuyển đổi Active và Standby`: Nếu router active gặp sự cố hoặc bị ngắt kết nối, router standby có độ ưu tiên cao nhất sẽ chuyển trở thành router active. Quá trình này diễn ra tự động và không làm gián đoạn quá trình hoạt động của mạng.

5. `Thời gian gián đoạn`: Trong quá trình chuyển đổi từ router active sang router standby, có một thời gian ngắn (thường chỉ trong vài giây) mà dữ liệu trên mạng có thể bị gián đoạn. Tuy nhiên, thời gian này là ngắn và không gây ra sự gián đoạn lớn cho dịch vụ mạng.


## Cấu hình

1. Các bước cấu hình

- `Xác định Virtual IP (VIP)`: Địa chỉ IP mà các thiết bị trong mạng sẽ sử dụng làm cổng gateway mặc định. Địa chỉ này sẽ được chia sẻ giữa các router trong một nhóm HSRP.

- `Xác định Router Priority`: Mỗi router trong nhóm HSRP sẽ có một độ ưu tiên. Router có độ ưu tiên cao nhất sẽ được chọn làm active. Nếu có nhiều router có cùng độ ưu tiên, router có địa chỉ IP cao nhất sẽ được chọn.

- `Cấu hình HSRP`: Cấu hình HSRP trên mỗi cổng của router bằng cách chỉ định IP VIP, độ ưu tiên và các thiết lập khác.

2. Cấu hình HSRP trên Router Cisco

- Trên Router R1 (active router)

```sh
R1(config)# interface GigabitEthernet0/0
R1(config-if)# no shut
R1(config-if)# ip address 192.168.1.1 255.255.255.0
R1(config-if)# standby 1 ip 192.168.1.254
R1(config-if)# standby 1 priority 110
```

-  Trên Router R2 (standby router)

```sh
R2(config)# interface GigabitEthernet0/0
R2(config-if)# no shut
R2(config-if)# ip address 192.168.1.2 255.255.255.0
R2(config-if)# standby 1 ip 192.168.1.254
R2(config-if)# standby 1 preempt
```
- Trong đó:

	+ `GigabitEthernet0/0` là cổng kết nối với mạng LAN.

	+ `192.168.1.1` là địa chỉ IP của router.

	+ `192.168.1.254` là địa chỉ IP Virtual của HSRP.

	+ `110` là độ ưu tiên của router trong HSRP.

## Kiểm tra cấu hình

```sh
Router# show standby brief
```
hoặc

```sh
Router# show running-config | include standby
```
==> Lệnh `show running-config | include standby` này sẽ hiển thị tất cả các dòng trong cấu hình hiện tại của router mà chứa từ "standby". Điều này bao gồm cấu hình HSRP trên các cổng của router và thông tin liên quan đến router active và standby.
