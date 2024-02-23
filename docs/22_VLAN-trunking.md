# VLAN trunking

## Một số khái niệm

- `VLAN trunking` là một tính năng quan trọng trong các mạng có nhiều VLAN, cho phép các dữ liệu từ nhiều VLAN được truyền qua một liên kết vật lý. 
Điều này giúp tối ưu hóa băng thông và cho phép các thiết bị mạng khác nhau truy cập vào các VLAN khác nhau.

- `Trunk port`: Là một cổng trên switch được cấu hình để truyền dữ liệu từ nhiều VLAN khác nhau. Các gói dữ liệu trên trunk port thường được gắn thêm thông tin về VLAN (VLAN tagging) để switch hoặc thiết bị mạng khác có thể phân biệt chúng.

- `VLAN Tagging`: Là quá trình thêm thông tin về VLAN vào các gói dữ liệu trên trunk port. Các thông tin này giúp cho các thiết bị mạng khác nhau có thể nhận biết và xử lý các gói dữ liệu thuộc về các VLAN khác nhau.

- `IEEE 802.1Q`: Là tiêu chuẩn VLAN trunking phổ biến nhất, trong đó các gói dữ liệu được gắn thêm thông tin về VLAN trực tiếp vào phần header của gói dữ liệu Ethernet

## VLAN Tagging

- `IEEE 802.1Q Tagging`: Đây là phương pháp phổ biến nhất được sử dụng trên hầu hết các mạng Ethernet ngày nay. Trong kỹ thuật này, một thẻ VLAN 802.1Q được thêm vào phần header của các gói dữ liệu Ethernet. Thẻ này bao gồm thông tin về VLAN ID, cho phép switch hoặc thiết bị mạng khác nhận biết và xử lý các gói dữ liệu thuộc về các VLAN khác nhau. Cơ chế này cho phép các gói dữ liệu từ nhiều VLAN được truyền qua cùng một liên kết vật lý.

- `ISL (Inter-Switch Link) Tagging`: Đây là một phương pháp tagging VLAN được Cisco phát triển trước khi 802.1Q trở thành tiêu chuẩn. ISL là một phương thức độc quyền của Cisco và không tương thích với các thiết bị không phải của Cisco. Trong ISL, toàn bộ khung Ethernet được bao bọc bởi một header ISL, trong đó chứa thông tin về VLAN ID và các thông tin khác. Mặc dù ISL không còn phổ biến như 802.1Q nhưng vẫn còn tồn tại trong một số mạng legacy Cisco.

## Các Mode Interface

- Trên các thiết bị mạng như switch hoặc router, có các mode interface khác nhau để cấu hình các cổng Ethernet. Dưới đây là một số mode interface phổ biến: 

1. `Access Mode`: Cổng trong access mode chỉ thuộc về một VLAN duy nhất và không thể truy cập các VLAN khác. Đây là mode phổ biến nhất được sử dụng cho các cổng kết nối với các thiết bị mạng như máy tính hoặc điểm truy cập Wi-Fi.

2. `Trunk Mode`: Cổng trong trunk mode có thể truyền dữ liệu từ nhiều VLAN thông qua một kết nối vật lý duy nhất. Các gói dữ liệu trên cổng này được gắn thêm thông tin về VLAN (VLAN tagging) để switch hoặc thiết bị mạng khác có thể phân biệt chúng. Trunk mode thường được sử dụng trên các liên kết giữa các switch hoặc giữa switch và router.

3. `Dynamic Auto Mode` và `Dynamic Desirable Mode`: Đây là các mode tự động mà cổng có thể tự động cấu hình là trunk hoặc access tùy thuộc vào cấu hình của cổng đối tác. Nếu cổng đối tác là trunk, cổng sẽ được cấu hình là trunk. Nếu cổng đối tác là access, cổng sẽ được cấu hình là access.

4. `VLAN Mode (SVI - Switched Virtual Interface)`: Đây là mode được sử dụng trên các thiết bị Layer 3 như router hoặc switch layer 3. Khi cấu hình SVI, một giao diện ảo được tạo ra để đại diện cho mỗi VLAN trên thiết bị. Giao diện này được sử dụng để cấu hình định tuyến hoặc các tính năng khác của Layer 3 trên VLAN đó.

5. `Port-Channel Mode`: Các port-channel hoặc etherchannel là nhóm các cổng vật lý được kết hợp lại để tạo thành một liên kết vật lý lớn hơn. Port-channel mode được sử dụng để cấu hình các nhóm port-channel.

## Cấu hình

- Lệnh cấu hình trunk port, sử dụng VLAN tagging với tiêu chuẩn 802.1Q

```sh
	Switch(config)# interface <interface_name>          //Chọn cổng muốn cấu hình là trunk
	Switch(config-if)# switchport mode trunk            //Thiết lập cổng là trunk mode
	Switch(config-if)# switchport trunk allowed vlan <vlan_list>   //Xác định các VLAN được phép truyền qua(tùy chọn)
```

- Trong đó:

	+ `<interface_name>`: Tên của cổng mà bạn muốn cấu hình là Trunk, ví dụ: GigabitEthernet0/1.

	+ `<vlan_list>`: Danh sách các VLAN được phép truyền qua cổng Trunk, có thể là một hoặc nhiều VLAN, hoặc cả tất cả các VLAN.

- Ví dụ

```sh
	Switch(config)# interface GigabitEthernet0/1
	Switch(config-if)# switchport mode trunk
	Switch(config-if)# switchport trunk allowed vlan 10,20,30
```

## Native VLAN

1. Khái niệm cơ bản

- Native VLAN là VLAN mặc định được sử dụng trên một liên kết trunk để truyền các gói dữ liệu không được gắn thẻ VLAN. Trong một cài đặt mạng VLAN, các gói dữ liệu được gắn thẻ VLAN thông thường được truyền qua các liên kết trunk với thông tin về VLAN ID được gắn vào header của gói dữ liệu. Tuy nhiên, có những trường hợp khi gói dữ liệu không được gắn thẻ VLAN, thì chúng sẽ được gửi qua mạng. Đây là lúc mà VLAN mặc định, hay Native VLAN, được sử dụng.

- `Đặc điểm quan trọng`: Native VLAN quan trọng trong môi trường mạng VLAN, vì nó đảm bảo việc truyền thông giữa các thiết bị trên mạng diễn ra một cách chính xác.

- `Mặc định và cấu hình`: Native VLAN thường được đặt là VLAN 1, nhưng bạn có thể thay đổi nó thành bất kỳ VLAN nào bạn muốn. Bạn cũng cần đảm bảo rằng Native VLAN được cấu hình giống nhau trên tất cả các thiết bị trong cùng một liên kết trunk.

- `Bảo mật`: Bạn nên chú ý đến bảo mật của Native VLAN, vì các tấn công như VLAN hopping có thể xảy ra khi một hacker sử dụng thông tin về Native VLAN để truy cập các VLAN khác trên mạng.

2. Cấu hình

- Câu lệnh để cấu hình

```sh
	Switch(config)# interface <interface_name>          
	Switch(config-if)# switchport trunk native vlan <vlan_id>
```

- Ví dụ

```sh
	Switch(config)# interface GigabitEthernet0/1          
	Switch(config-if)# switchport trunk native vlan 20
```
==> Trong ví dụ này, VLAN 20 được đặt là Native VLAN trên cổng GigabitEthernet0/1

## Kiểm tra cấu hình

- Hiển thị thông tin về các trunk port trên switch

```sh
	switch# show interfaces trunk
```

- Kiểm tra cấu hình cụ thể của một port

```sh
	switch# show running-config interface <interface_name>
```