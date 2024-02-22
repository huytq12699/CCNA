# Định tuyến tĩnh (Static Route)

1. Tìm hiểu về định tuyến tĩnh

- Static Route là một phần quan trọng trong mạng máy tính, được sử dụng để xác định các đường đi cụ thể cho các gói dữ liệu trong mạng. Khi một thiết bị mạng nhận được một gói dữ liệu, nó sẽ kiểm tra bảng định tuyến của mình để quyết định phải gửi gói đó đi đâu.

- Static Route được cấu hình bằng cách thủ công bởi người quản trị mạng. Người quản trị sẽ chỉ định các đường đi cụ thể cho các mạng hoặc host nhất định. Mỗi một static route bao gồm `địa chỉ đích (destination address)`, `subnet mask` để xác định phạm vi của mạng, và `địa chỉ IP của router(hoặc giao diện mạng)` mà gói dữ liệu sẽ được chuyển đến.

2. Ưu và nhược điểm

- Ưu điểm: độ tin cậy cao và dễ dàng cấu hình

- Nhược điểm: nó không linh hoạt như Dynamic Routing (định tuyến động) và yêu cầu người quản trị phải thủ công cập nhật và duy trì bảng định tuyến.

3. Cấu hình Static Route

- Có 2 cách cấu hình Static Route

		- Cách 1: cấu hình theo "next hop" address

			```sh
 			Router(config)#ip route địa_chỉ_mạng_muốn_quảng_bá subnet_mask địa_chỉ_ip_của_interface_nối_với_mạng_muốn_quảng_bá
			```
		- Cách 2: Cấu hình theo exit interface

			```sh
			Router(config)#ip route địa_chỉ_mạng_muốn_quảng_bá subnet_mask interface_nối_với_mạng_muốn_quảng_bá
			```
- Cấu hình Default Route

			```sh
			Router(config)#ip route 0.0.0.0 0.0.0.0 [exit interface/ip address]
			```

4. Kiểm tra cấu hình

- Để kiểm tra cấu hình Static Route trên một thiết bị mạng, bạn cần sử dụng các lệnh thích hợp tùy thuộc vào loại thiết bị mạng bạn đang sử dụng. Dưới đây là một số lệnh phổ biến được sử dụng trên các thiết bị mạng như router hoặc switch:

	+ Kiểm tra bảng định tuyến (Routing Table): Trên các router hoặc switch chạy hệ điều hành Cisco IOS, bạn có thể sử dụng lệnh `show ip route` để hiển thị bảng định tuyến IPv4 và `show ipv6 route` để hiển thị bảng định tuyến IPv6.

	+ Kiểm tra cấu hình Static Route: Trên Cisco IOS, bạn có thể sử dụng lệnh `show running-config` hoặc `show ip route static` để hiển thị cấu hình các static route đã được cấu hình trên thiết bị.

	+ Kiểm tra thông tin chi tiết về một static route cụ thể: Sử dụng lệnh `show ip route [địa chỉ mạng]` để hiển thị thông tin chi tiết về một static route cụ thể.
