# Định tuyến tĩnh (Static Route)

## Tìm hiểu về định tuyến tĩnh

1. Khái niệm

- `Static Route` là một phần quan trọng trong mạng máy tính, được sử dụng để xác định các đường đi cụ thể cho các gói dữ liệu trong mạng. Khi một thiết bị mạng nhận được một gói dữ liệu, nó sẽ kiểm tra bảng định tuyến của mình để quyết định phải gửi gói đó đi đâu.

- Static Route được cấu hình bằng cách thủ công bởi người quản trị mạng. Người quản trị sẽ chỉ định các đường đi cụ thể cho các mạng hoặc host nhất định. 

- Mỗi một static route bao gồm địa chỉ đích (destination address), subnet mask để xác định phạm vi của mạng, và địa chỉ IP của router(hoặc giao diện mạng) mà gói dữ liệu sẽ được chuyển đến.

2. Ưu và nhược điểm

- Ưu điểm: độ tin cậy cao và dễ dàng cấu hình

- Nhược điểm: nó không linh hoạt như Dynamic Routing (định tuyến động) và yêu cầu người quản trị phải thủ công cập nhật và duy trì bảng định tuyến.

## Cấu hình Static Route

1. Có 2 cách cấu hình Static Route

- Cách 1: cấu hình theo next hop address

```sh
Router(config)# ip route <ip_destination_network> <subnet_mask> <next_hop_address>
```

- Cách 2: Cấu hình theo exit interface

```sh
Router(config)# ip route <ip_destination_network> <subnet_mask> <interface_id>
```

2. Cấu hình Default Route

```sh
Router(config)#ip route 0.0.0.0 0.0.0.0 [exit interface/ip address]
```

## Kiểm tra cấu hình

1. Kiểm tra bảng định tuyến (Routing Table)

```sh
Router# show ip route 		//hiển thị bảng định tuyến IPv4 

	hoặc

Router# show ipv6 route 	//hiển thị bảng định tuyến IPv6
```

2. Kiểm tra cấu hình Static Route 

```sh
Router# show running-config

	hoặc 

Router# show ip route static
```
