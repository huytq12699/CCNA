# EIGRP (Enhanced Interior Gateway Routing Protocol)

- EIGRP là viết tắt của "Enhanced Interior Gateway Routing Protocol" (Giao thức Định tuyến Cổng Nội bộ Nâng cao). 
Đây là một giao thức định tuyến nội bộ được sử dụng trong mạng máy tính để định tuyến gói tin giữa các mạng con của một mạng lớn hơn. 
EIGRP được phát triển bởi Cisco và là một phần của giao thức định tuyến nội bộ của Cisco.

- Một số điểm nổi bật về EIGRP bao gồm:
	+ Tính linh hoạt và hiệu quả: EIGRP sử dụng thuật toán DUAL (Diffusing Update Algorithm) để đảm bảo định tuyến tốt nhất và lựa chọn con đường tốt nhất cho việc truyền tải dữ liệu. Nó cũng hỗ trợ nhiều phương thức kết nối như Ethernet, Frame Relay và ATM.

	+ Convergence nhanh: EIGRP cung cấp thời gian hội tụ (convergence) nhanh hơn so với một số giao thức khác như RIP (Routing Information Protocol) hay OSPF (Open Shortest Path First), giúp đảm bảo rằng mạng có thể chịu được sự thay đổi cấu trúc nhanh chóng.

	+ Thiết kế cho mạng lớn và phức tạp: EIGRP được thiết kế để hoạt động hiệu quả trên các mạng lớn và phức tạp, với khả năng chia nhỏ mạng thành các vùng định tuyến riêng biệt để quản lý mạng lưới lớn hơn.

	+ Bảo mật: EIGRP cung cấp các cơ chế bảo mật như xác thực mật khẩu để ngăn chặn các cuộc tấn công giả mạo hoặc xâm nhập vào hệ thống định tuyến.

## Cấu hình EIGRP

1. Cấu hình cơ bản

```sh 
Router(config)#router eigrp eigrp_muốn_đặt ( 1->65535) 
Router(config-router)#network IP_mạng_muốn_quảng_bá 
Router(config-router)#no auto-summary (ko tự ghép các dải địa chỉ IP thành 1 dải lớn)
``` 

- Ví dụ:
```sh
Router(config)# router eigrp 100                          // Bắt đầu cấu hình EIGRP, số 100 là Autonomous System (AS) number
Router(config-router)# network 192.168.1.0                // Kích hoạt EIGRP trên mạng con 192.168.1.0
Router(config-router)# network 10.0.0.0                   // Kích hoạt EIGRP trên mạng con 10.0.0.0
Router(config-router)# network 172.16.0.0                  // Kích hoạt EIGRP trên mạng con 172.16.0.0
Router(config-router)# no auto-summary 				//(ko tự ghép các dải địa chỉ IP thành 1 dải lớn)
Router(config-router)# exit                                // Thoát khỏi chế độ cấu hình EIGRP
Router(config)# exit                                        // Thoát khỏi chế độ cấu hình
Router# copy running-config startup-config                   // Lưu cấu hình vào bộ nhớ non-volatile
```

> Ở ví dụ trên:

+ Chúng ta bắt đầu bằng việc vào chế độ cấu hình EIGRP với lệnh `router eigrp 100`, trong đó "100" là Autonomous System (AS) number của EIGRP.

+ Bằng cách sử dụng lệnh `network`, chúng ta kích hoạt EIGRP trên các mạng con cụ thể. Cụ thể, EIGRP được kích hoạt trên mạng con `192.168.1.0`, `10.0.0.0` và `172.16.0.0`.

+ Sau khi hoàn thành cấu hình, chúng ta thoát khỏi chế độ cấu hình và lưu cấu hình vào bộ nhớ `non-volatile` với lệnh `copy running-config startup-config`

2. Thay đổi băng thông và tự tổng hợp tuyến trong interface

```sh
Router(config-if)#bandwidth kilobits 
Router(config-if)#ip summary-address protocol AS network number subnets mask 
```

3. Cân bằng tải trong EIGRP
 
	`Router(config-router)#variance number`

4. Quảng bá default route

- Cách 1:  
`Router(config)#ip route 0.0.0.0 0.0.0.0 [interface/nexthop]` 
`Router(config)#redistribute static`

- Cách 2:  
`Router(config)#ip default-network network number`

- Cách 3:  
`Router(config-if)#ip summary-network eigrp AS number 0.0.0.0 0.0.0.0`
 
5. Quảng bá các tuyến khác trong EIGRP (không phải là default)

```sh 
		Router(config-router)#redistribute giao_thức_muốn_quảng_bá ID_metrics k1 k2 k3 k4 k5
		VD: Router(config-router)#redistribute ospf metrics 100 100 100 100 100
```
6. Chia sẻ traffic trong EIGRP

	`Router(config-router)#traffic share {balanced/min}`

## Các lệnh kiểm tra cấu hình EIGRP

- `show ip protocols`: Hiển thị các thông tin tổng quan về các giao thức định tuyến đang chạy trên thiết bị, bao gồm EIGRP.

- `show ip eigrp neighbors`: Liệt kê các hàng xóm EIGRP (các thiết bị khác mà thiết bị của bạn đang trao đổi thông tin định tuyến với) cùng với các thông tin liên quan như địa chỉ IP, AS number, uptime...

- `show ip eigrp interfaces`: Hiển thị thông tin về các giao diện mạng mà EIGRP đang hoạt động trên thiết bị, bao gồm trạng thái của giao diện và các metric được sử dụng.

- `show ip eigrp topology`: Hiển thị bảng định tuyến EIGRP, cho biết con đường tốt nhất đến các mạng đích cụ thể.

- `show ip eigrp topology all-links`: Hiển thị bảng định tuyến EIGRP bao gồm tất cả các con đường, kể cả các con đường backup.

- `show ip eigrp traffic`: Hiển thị lưu lượng EIGRP đang đi qua thiết bị, giúp theo dõi hiệu suất của giao thức.

- `debug eigrp packets`: Bật gỡ lỗi để xem các gói tin EIGRP đang được truyền qua thiết bị. Lưu ý rằng việc sử dụng debug có thể tăng tải cho thiết bị, nên cần sử dụng cẩn thận.