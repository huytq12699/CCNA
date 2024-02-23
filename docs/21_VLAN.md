# Virtual Local Area Network (VLAN)

## Khái niệm

- Là một công nghệ mạng cho phép bạn chia một mạng vật lý thành nhiều mạng ảo độc lập, gọi là các VLAN, mà không cần phải thay đổi cấu trúc vật lý của mạng. Điều này cho phép bạn phân chia mạng theo các nhóm hoặc chức năng khác nhau mà không cần phải cắt mạng vật lý.

## Đặc điểm cơ bản

1. `Isolation (Cách ly)`: Các VLAN cho phép bạn tạo ra các phân đoạn mạng vật lý mà không có sự tương tác giữa chúng. Điều này giúp tăng cường bảo mật và quản lý mạng.

2. `Segmentation (Phân đoạn)`: Bằng cách phân chia mạng thành các VLAN, bạn có thể quản lý mạng hiệu quả hơn bằng cách chia nhỏ mạng thành các phân đoạn nhỏ hơn, giảm tải băng thông và làm cho mạng trở nên linh hoạt hơn.

3. `Broadcast Control (Kiểm soát Broadcast)`: Mỗi VLAN hoạt động như một mạng LAN riêng biệt, giúp giảm lượng gói tin broadcast trên mạng.

4. `Security (Bảo mật)`: VLAN cung cấp một cơ chế để kiểm soát truy cập vào mạng bằng cách áp dụng các chính sách bảo mật trên mỗi VLAN.

5. `Flexibility (Lin động)`: Các VLAN có thể được cấu hình và quản lý một cách linh hoạt, cho phép dễ dàng thêm, sửa đổi hoặc xóa bỏ chúng tùy thuộc vào nhu cầu mạng.

6. `Performance (Hiệu suất)`: Bằng cách phân chia mạng thành các VLAN, bạn có thể tối ưu hóa hiệu suất mạng bằng cách giảm lưu lượng mạng không cần thiết và cải thiện khả năng truy cập và chuyển tiếp dữ liệu.

==> Cài đặt và quản lý VLAN thường được thực hiện thông qua thiết bị mạng như switch hoặc router, nơi bạn có thể cấu hình cổng để thuộc về một hoặc nhiều VLAN.

## VLAN ID

- VLAN ID (Identifier) là một số nguyên dương dùng để định danh và phân biệt các VLAN khác nhau trên mạng. Mỗi VLAN sẽ được gán một VLAN ID duy nhất để phân biệt nó với các VLAN khác trong hệ thống.

- VLAN ID có thể là một con số từ 1 đến 4094, tuy nhiên có một số VLAN ID đặc biệt. Cụ thể:

	+ `VLAN 0`: VLAN 0 được sử dụng để chỉ các cổng trung tâm của một thiết bị mạng.

	+ `VLAN 1`: Mặc định, VLAN 1 thường được sử dụng cho giao tiếp quản lý và không nên được xóa hoặc sửa đổi trừ khi cần thiết.

	+ `VLAN 2 -> VLAN 1001`: có thể dùng để tạo, sửa, xóa

	+ `VLAN 1002 đến VLAN 1005`: Các VLAN này thường được dành cho các giao thức FDDI và Token Ring và không thường được sử dụng trong môi trường mạng Ethernet hiện đại.

	+ `VLAN 1006-> VLAN 4094`: các VLAN mở rộng.

## Cấu hình VLAN

1. Tạo VLAN

```sh
	switch(config)# vlan <vlan_id>
	switch(config-vlan)# name <tên_tự_chọn> // không bắt buộc
```

2. Gán cổng vào VLAN

- Gán vào 1 cổng

```sh
	Switch(config)#interface <cổng_tương_ứng>
	Switch(config-int)#switchport access vlan <vlan-id> 
```

- Gán vào nhiều cổng cùng một lúc

```sh
	switch(config)# interface range <cổng 1,2,3 ...>
	switch(config-if-range)# switchport mode access
	switch(config-if-range)# switchport access vlan <vlan-id>
```

3. Ví dụ

 - Tạo một VLAN với VLAN ID 10 và gán các cổng fa0/1, fa0/2 trên Switch tương ứng VLAN

```sh
	switch(config)# vlan 10
	switch(config-vlan)# name VLAN10
	switch(config)# interface range fa0/1 - 2
	switch(config-if-range)# switchport mode access
	switch(config-if-range)# switchport access vlan 10
```
- Trong đó:

	+ `interface range fa0/1 - 2` cho phép bạn chọn một dãy các cổng (trong trường hợp này là cổng 1 và 2). 

	+ `switchport mode access` cấu hình cổng là chế độ truy cập.

	+ `switchport access vlan 10` gán cổng vào VLAN 10.

## Kiểm tra cấu hình

1. Hiển thị thông tin VLAN hiện tại

```sh
	show vlan
```
2. Hiển thị thông tin giao diện cổng

```sh
	show interfaces status
```
3. Hiển thị thông tin chi tiết về một VLAN cụ thể

```sh
	show vlan id [VLAN_ID]
```

4. Kiểm tra giao diện cổng đang được gán vào VLAN

```sh
	show interfaces [interface_id] switchport
```

5. Kiểm tra cấu hình toàn bộ

```sh
	show running-config
```
