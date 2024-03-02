# Ether Channel

##  Khái niệm, mục đích sử dụng

1. Khái niệm: Là một tính năng trong mạng máy tính cho phép bạn kết hợp nhiều kết nối vật lý giữa hai thiết bị mạng (chẳng hạn như switch-switch, switch-router) thành một liên kết logic duy nhất có băng thông cao hơn và cung cấp tính sẵn sàng cao hơn.

2. Mục đích sử dụng:

- `Tăng băng thông`: Bằng cách kết hợp nhiều kết nối vật lý, EtherChannel có thể cung cấp băng thông lớn hơn so với một kết nối vật lý duy nhất.

- `Tăng tính sẵn sàng`: Nếu một trong các kết nối trong EtherChannel gặp sự cố, các kết nối còn lại vẫn có thể tiếp tục hoạt động, giảm thiểu thời gian ngưng trệ và tăng tính sẵn sàng của mạng.

- `Cải thiện cân bằng tải`: EtherChannel có thể được cấu hình để cân bằng tải giao lưu các gói dữ liệu qua các kết nối thành viên của nó, giúp tối ưu hóa sử dụng băng thông.

## Điều kiện thực hiện

- `Các cổng thành viên cần phải cùng tốc độ`: Tất cả các cổng Ethernet trong EtherChannel cần phải chạy ở cùng một tốc độ. Ví dụ, nếu bạn muốn tạo một EtherChannel bằng cách kết hợp hai cổng GigabitEthernet, cả hai cổng này cần phải chạy ở tốc độ GigabitEthernet.

- `Phải cùng duplex mode`: Các cổng thành viên trong EtherChannel cũng cần phải chạy ở cùng một chế độ duplex (chẳng hạn như full-duplex). Sự không đồng nhất về duplex mode có thể dẫn đến lỗi giao tiếp và giảm hiệu suất.

- `Giao thức EtherChannel phải được đồng bộ`: Nếu bạn sử dụng giao thức EtherChannel như PAgP hoặc LACP, cả hai đầu của EtherChannel cần được cấu hình để sử dụng cùng một giao thức. Nếu một bên sử dụng PAgP trong khi bên kia sử dụng LACP, EtherChannel sẽ không hoạt động.

- `Các cổng thành viên phải cùng cấu hình`: Trước khi thêm các cổng vào EtherChannel, bạn cần đảm bảo rằng chúng có cùng cấu hình. Điều này bao gồm cùng một phương thức đóng gói VLAN, cùng một native VLAN (nếu áp dụng), và cùng một chế độ hoạt động (trunk, access, hoặc dynamic).

- `Tất cả các cổng thành viên phải ở cùng một thiết bị`: EtherChannel chỉ hoạt động giữa các cổng trên cùng một thiết bị mạng. Không thể tạo EtherChannel giữa các cổng trên các thiết bị khác nhau.

- `Các cổng thành viên cần kết nối với cùng một mạng hoặc thiết bị`: Để tận dụng băng thông lớn hơn của EtherChannel, các cổng thành viên thường được kết nối với cùng một mạng hoặc thiết bị.

## Các giao thức cấu hình

- Có 2 giao thức phổ biến được sử dụng để cấu hình Ether Channel

1. `PAgP (Port Aggregation Protocol)`

- Đây là giao thức độc quyền của Cisco, cho phép các cổng Ethernet đàm phán với nhau để xác định xem liệu chúng có thể được kết hợp thành một EtherChannel hay không. PAgP tự động kiểm tra các cổng Ethernet đối tác và tự động thực hiện EtherChannel nếu cả hai bên đều được cấu hình để hỗ trợ PAgP và được cấu hình chính xác.

2. `LACP (Link Aggregation Control Protocol)`

- LACP là một tiêu chuẩn được định nghĩa trong IEEE 802.3ad, cho phép các thiết bị mạng của nhiều nhà sản xuất khác nhau tạo ra EtherChannel một cách thống nhất. LACP hoạt động bằng cách gửi các tin nhắn LACP giữa các thiết bị và đàm phán EtherChannel. LACP thường được sử dụng khi kết nối các thiết bị Cisco với các thiết bị không phải của Cisco.

## Cấu hình 

- Lệnh cấu hình PAgP

```sh
Switch(config)# interface range <dãy các cổng>    			//Chọn các cổng thành viên
Switch(config-if-range)# channel-group 1 mode desirable    	//Tạo EtherChannel với PAgP <desirable | auto>
Switch(config)# interface port-channel 1               		//Chọn cổng EtherChannel
Switch(config-if)# switchport trunk encapsulation dot1q  	//Thiết lập giao thức đóng gói VLAN trên EtherChannel(nếu cần)
Switch(config-if)# switchport mode trunk              		//Thiết lập EtherChannel là trunk port(nếu cần)
```
- Lệnh cấu hình LACP

```sh
Switch(config)# interface range <dãy các cổng>    			//Chọn các cổng thành viên
Switch(config-if-range)# channel-group 1 mode active        //Tạo EtherChannel với LACP <active | passive>
Switch(config)# interface port-channel 1               		//Chọn cổng EtherChannel
Switch(config-if)# switchport trunk encapsulation dot1q  	//Thiết lập giao thức đóng gói VLAN trên EtherChannel(nếu cần)
Switch(config-if)# switchport mode trunk              		//Thiết lập EtherChannel là trunk port(nếu cần)
```

- Ví dụ sử dụng LACP

```sh
	Switch(config)# interface range GigabitEthernet0/1 - 2  
	Switch(config-if-range)# channel-group 1 mode active    
	Switch(config-if-range)# exit
	Switch(config)# interface port-channel 1               		
	Switch(config-if)# switchport trunk encapsulation dot1q  
	Switch(config-if)# switchport mode trunk              			
```

==> Ở ví dụ trên:

+ Các cổng GigabitEthernet 0/1 và 0/2 được kết hợp thành một EtherChannel với giao thức LACP và được đánh số là Port-channel 1.

+ EtherChannel được cấu hình là trunk port và được thiết lập để đóng gói VLAN theo tiêu chuẩn 802.1Q.

## Kiểm tra cấu hình

1. Kiểm tra cấu hình EtherChannel

```sh
	Switch# show etherchannel summary
```

2. Kiểm tra cấu hình của một EtherChannel cụ thể

```sh
	Switch# show etherchannel <channel_number> 
```

3. Kiểm tra chi tiết cấu hình của tất cả các cổng EtherChannel

```sh
	Switch# show running-config interface port-channel
```