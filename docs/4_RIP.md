# RIP (Routing Information Protocol)

- RIP viết tắt của "Routing Information Protocol" (Giao thức Thông tin Định tuyến), là một giao thức định tuyến phổ biến được sử dụng trong mạng máy tính. Đặc biệt, RIP là một trong những giao thức định tuyến đơn giản nhất và phổ biến nhất trong các mạng nhỏ và trung bình.

- Một số điểm nổi bật về RIP

+ Giao thức định tuyến vector đơn: RIP là một giao thức định tuyến vector đơn (hoặc còn được gọi là giao thức định tuyến Bellman-Ford), nghĩa là nó đưa ra quyết định định tuyến dựa trên số lượng nhảy (hops) để đến mạng đích.

+ Giới hạn số lượng nhảy: RIP giới hạn số lượng nhảy tối đa mà một gói tin có thể đi qua trong mạng, thường là 15 nhảy. Điều này giới hạn phạm vi mạng mà RIP có thể hỗ trợ, và trong một số trường hợp, nó có thể dẫn đến hiện tượng loop.

+ Cập nhật định kỳ: RIP sử dụng cập nhật định kỳ (cứ một khoảng thời gian nhất định) để truyền tải thông tin định tuyến. Thời gian cập nhật mặc định là 30 giây.

+ Metric: RIP sử dụng metric là số lượng nhảy (hops) để đo lường khoảng cách đến mạng đích. Mạng với số lượng nhảy ít nhất sẽ được chọn làm con đường tốt nhất.

+ Khả năng chịu lỗi thấp: Mặc dù RIP dễ triển khai và sử dụng, nhưng nó có khả năng chịu lỗi thấp và hiệu suất kém trên các mạng lớn và phức tạp. Đặc biệt, việc sử dụng cập nhật định kỳ có thể tạo ra lưu lượng mạng không cần thiết.

+ RIP v1 và RIP v2: Có hai phiên bản chính của RIP: RIP v1 và RIP v2. RIP v2 hỗ trợ định tuyến chia sẻ mạng con (subnetting) và bảo mật thông qua sử dụng các phương thức xác thực.

## Cấu hình RIP

```sh
	Router(config)#router rip (dùng giao thức định tuyến RIP) 
	Router(config-router)#network địa_chỉ_ip (địa chỉ mạng muốn quảng bá bằng giao thức RIP)
	Router(config-router)#no auto-summary
	Router(config-router)#passive-interface tên_cổng (thông tin định tuyến RIP ko đc gửi ra cổng này) 
	Router(config-router)#version 2 (dùng RIP version 2, mặc định là version 1) 
```
- Ví dụ:

```sh
Router(config)# router rip
Router(config-router)# version 2                      // Cấu hình sử dụng RIP version 2 (tùy chọn)
Router(config-router)# network 192.168.1.0            // Kích hoạt RIP trên mạng con 192.168.1.0
Router(config-router)# network 10.0.0.0               // Kích hoạt RIP trên mạng con 10.0.0.0
Router(config-router)# no auto-summary                // Vô hiệu hóa tự động tóm tắt địa chỉ
Router(config-router)# passive-interface G0/0  	// Chỉ định giao diện nào là giao diện chủ động (tùy chọn)
Router(config-router)# passive-interface G0/1  // Chỉ định giao diện nào là giao diện chủ động (tùy chọn)
Router(config-router)# exit                           // Thoát khỏi chế độ cấu hình RIP
Router(config)# exit                                  // Thoát khỏi chế độ cấu hình toàn bộ
Router# copy running-config startup-config            // Lưu cấu hình vào bộ nhớ non-volatile
```
> Trong ví dụ này:

1. Đầu tiên, chúng ta đi vào chế độ cấu hình RIP bằng lệnh `router rip`.

2. Tiếp theo, chúng ta cấu hình sử dụng RIP version 2 bằng lệnh `version 2`(tùy chọn, nếu không chỉ định, RIP sẽ sử dụng phiên bản mặc định là RIP version 1).

3. Chúng ta kích hoạt RIP trên các mạng con cụ thể bằng lệnh `network`. Trong ví dụ này, RIP được kích hoạt trên mạng con `192.168.1.0` và `10.0.0.0`.

4. Lệnh `no auto-summary` được sử dụng để vô hiệu hóa tự động tóm tắt các mạng con.

5. Cuối cùng, chúng ta có thể sử dụng lệnh `passive-interface` để chỉ định các giao diện mà RIP sẽ không gửi gói tin RIP trên đó (tùy chọn).
Sau khi hoàn thành cấu hình, chúng ta thoát khỏi chế độ cấu hình và lưu cấu hình vào bộ nhớ `non-volatile` bằng lệnh `copy running-config tartup-config`

## Các lệnh kiểm tra cấu hình RIP

- `show ip protocols`: Hiển thị các thông tin tổng quan về các giao thức định tuyến đang chạy trên thiết bị, bao gồm cấu hình RIP.

- `show ip route`: Hiển thị bảng định tuyến IP, bao gồm các mạng mà thiết bị đã học thông qua RIP.

- `show ip rip database`: Hiển thị cơ sở dữ liệu định tuyến RIP trên thiết bị, bao gồm các mạng đã học, metric và next hop.

- `show ip rip neighbors`: Liệt kê các hàng xóm RIP (các thiết bị khác mà thiết bị của bạn đang trao đổi thông tin định tuyến với) cùng với các thông tin liên quan như địa chỉ IP và thời gian kết nối.

- `debug ip rip`: Bật gỡ lỗi để xem các gói tin RIP đang được truyền qua thiết bị. Lưu ý rằng việc sử dụng debug có thể tăng tải cho thiết bị, nên sử dụng cẩn thận và chỉ khi cần thiết.


