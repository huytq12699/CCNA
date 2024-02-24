# Multi-Protocol Label Switching (MPLS)

## Tìm hiểu chung

1. Khái niệm

- Chuyển Mạch Nhãn Đa Giao Thức (MPLS) là một công nghệ mạng phức tạp được sử dụng để cải thiện hiệu suất và quản lý của các mạng truyền thông dữ liệu. 

- MPLS thường được triển khai trong các mạng WAN (Wide Area Network) và cung cấp khả năng định tuyến dựa trên nhãn (label) thay vì dựa trên địa chỉ IP truyền thống.

2. Đặc điểm

- `Chuyển mạch dựa trên nhãn (Label Switching)`: MPLS sử dụng các nhãn (label) để xác định con đường mà dữ liệu sẽ di chuyển thông qua mạng. Mỗi gói tin được đánh nhãn khi đi vào mạng MPLS và các thiết bị chuyển mạch MPLS (như các router MPLS) sử dụng nhãn này để xác định con đường cho gói tin.

- `Khả năng định tuyến dựa trên nhãn`: MPLS cho phép các nhãn được gán cho các gói tin dựa trên các tiêu chí như chất lượng dịch vụ (QoS), yêu cầu định tuyến, và các điều kiện mạng khác. Điều này cung cấp khả năng định tuyến linh hoạt và quản lý dữ liệu hiệu quả hơn.

- `Tích hợp dịch vụ`: MPLS có khả năng hỗ trợ nhiều dịch vụ mạng khác nhau trên cùng một hạ tầng, bao gồm VPN (Virtual Private Network), truyền thông âm thanh và video, và các ứng dụng truyền thông dữ liệu khác.

- `Quản lý mạng hiệu quả`: MPLS cung cấp các công cụ quản lý mạng mạnh mẽ, bao gồm quản lý lưu lượng, giám sát mạng và khả năng chẩn đoán lỗi.

## Cách thức hoạt động

1. `Gán Nhãn (Label Assignment)`:

- Khi một gói tin vào mạng MPLS, thiết bị đầu cuối (như router hoặc switch) sẽ gán một nhãn MPLS cho gói tin. Nhãn này được sử dụng để xác định con đường của gói tin thông qua mạng.

2. `Chuyển Mạch Nhãn (Label Switching)`:

- Khi gói tin đã được gán nhãn, các thiết bị chuyển mạch MPLS (như các router hoặc switch) sử dụng nhãn này để xác định con đường cho gói tin. Thay vì sử dụng địa chỉ IP để xác định con đường, các thiết bị chuyển mạch MPLS sử dụng nhãn để nhanh chóng và hiệu quả chuyển tiếp gói tin.

3. `Định Tuyến Dựa Trên Nhãn (Label-Based Routing)`:

- Các thiết bị chuyển mạch MPLS sử dụng thông tin trong nhãn để định tuyến gói tin. Nhãn này có thể chỉ định con đường cụ thể hoặc chỉ định cho một nhóm con đường (như một FEC - Forwarding Equivalence Class).

4. `Loại Bỏ Nhãn (Label Popping)`:

- Khi gói tin đến đích cuối cùng, nhãn MPLS sẽ được loại bỏ và gói tin sẽ được chuyển tiếp theo cách thông thường (dựa trên địa chỉ IP hoặc giao thức mạng khác).

==> MPLS cho phép tạo ra các kết nối đường truyền ảo và cung cấp khả năng định tuyến linh hoạt dựa trên nhãn. Điều này giúp cải thiện hiệu suất và quản lý của mạng, đặc biệt là trong các môi trường mạng phức tạp có nhu cầu độ trễ thấp và chất lượng dịch vụ cao.

## Cấu hình MPLS

- Cấu hình MPLS trên một router Cisco IOS

1. Bật MPLS trên router

```sh
Router(config)# mpls ip
```

2. Bật Label Distribution Protocol (LDP)

```sh
Router(config)# mpls ldp router-id loopback0
Router(config)# interface loopback0
Router(config-if)# ip address 10.0.0.1 255.255.255.255
```

3. Cấu hình các giao diện có thể MPLS Forwarding

```sh
Router(config)# interface <interface-type> <interface-number>
Router(config-if)# mpls ip

```

4. Cấu hình các định tuyến MPLS (tuỳ chọn: Static Route, RIP, OSPF, EIGRP)

ví dụ ta dùng Static Route

```sh
Router(config)# ip route <destination-network> <subnet-mask> <next-hop-address>
```

==> Trong ví dụ trên:

	+ Bước 1: bật MPLS trên router.

	+ Bước 2: bật LDP và cấu hình router ID cho LDP sử dụng địa chỉ loopback.

	+ Bước 3: cấu hình các giao diện để chấp nhận và chuyển tiếp gói tin MPLS.

	+ Bước 4: cấu hình định tuyến MPLS (tuỳ chọn).

## Kiểm tra cấu hình

```sh
Router# show mpls interfaces
```

hoặc

```sh
Router# show mpls forwarding-table
```