# OSPF (Open Shortest Path First)

- OSPF là một giao thức định tuyến nội bộ phổ biến được sử dụng trong mạng máy tính để định tuyến gói tin giữa các mạng con của một mạng lớn hơn.

- Giao thức mạng lớp 3: OSPF là một giao thức mạng lớp 3, nghĩa là nó hoạt động ở lớp Network Layer của mô hình OSI. Nó sử dụng các gói tin định tuyến để trao đổi thông tin định tuyến giữa các thiết bị định tuyến.

- Tính mạnh mẽ và phức tạp: OSPF là một giao thức mạnh mẽ và phức tạp, được thiết kế để hoạt động hiệu quả trên các mạng lớn và phức tạp. Nó cung cấp nhiều tính năng như load balancing, route summarization và hỗ trợ VLSM (Variable Length Subnet Masking).

- Link-State Protocol: OSPF là một giao thức dựa trên trạng thái liên kết (Link-State Protocol), điều này có nghĩa là các thiết bị OSPF (routers) trao đổi thông tin về trạng thái của các liên kết mạng với nhau. Dựa trên thông tin này, OSPF xây dựng bảng định tuyến mạng toàn cục.

- Dựa trên thuật toán SPF: OSPF sử dụng thuật toán SPF (Shortest Path First) để tính toán con đường tối ưu giữa các mạng. Thuật toán này chọn ra con đường ngắn nhất (shortest path) từ một node đến tất cả các node còn lại trên mạng.

- Phân vùng (Areas): OSPF sử dụng khái niệm phân vùng (areas) để tăng hiệu suất và giảm bớt overhead trong mạng lớn. Các phân vùng này giúp giảm độ phức tạp của các bảng định tuyến và giảm lưu lượng định tuyến.

- Bảo mật: OSPF hỗ trợ nhiều cơ chế bảo mật như xác thực mật khẩu và xác thực khóa công cộng để ngăn chặn các cuộc tấn công giả mạo hoặc xâm nhập vào hệ thống định tuyến.

## Cấu hình OSPF

- Cấu hình cơ bản

```sh
Router(config)#router ospf ospf_process ID ( 1->65535) 
Router(config-router)#network dải_đại_chỉ_muốn_quảng_bá Wildcard_mask area_ID
```

- Ví dụ:
```sh
Router(config)# router ospf 1                                // Bắt đầu cấu hình OSPF, số 1 là OSPF process ID
Router(config-router)# network 192.168.1.0 0.0.0.255 area 0  // Kích hoạt OSPF trên mạng con 192.168.1.0/24, trong khu vực 0
Router(config-router)# network 10.0.0.0 0.255.255.255 area 0 // Kích hoạt OSPF trên mạng 10.0.0.0/8, trong khu vực 0
Router(config-router)# network 172.16.0.0 0.0.255.255 area 1 // Kích hoạt OSPF trên mạng 172.16.0.0/16, trong khu vực 1
Router(config-router)# exit                                    // Thoát khỏi chế độ cấu hình OSPF
Router(config)# exit                                          // Thoát khỏi chế độ cấu hình
Router# copy running-config startup-config                    // Lưu cấu hình vào bộ nhớ non-volatile
```

> Ở ví dụ trên:

1. Chúng ta bắt đầu bằng việc vào chế độ cấu hình OSPF với lệnh `router ospf 1`, trong đó "1" là `OSPF process ID`.
2. Bằng cách sử dụng lệnh `network`, chúng ta kích hoạt OSPF trên các mạng con cụ thể. 
Cụ thể, OSPF được kích hoạt trên mạng con `192.168.1.0/24`, `10.0.0.0/8` và `172.16.0.0/16`.
3. Sau khi hoàn thành cấu hình, chúng ta thoát khỏi chế độ cấu hình và lưu cấu hình vào bộ nhớ `non-volatile` với lệnh `copy running-config startup-config`

- Cấu hình quảng bá một tuyến mặc định (default) trong OSPF 

`Router(config-router)#default-information originate`

- Cấu hình quảng bá một tuyến khác (không phải là default) 

`Router(config-router)#redistribute protocols subnets`

## Các lệnh kiểm tra cấu hình

- `show ip protocols`: Hiển thị cấu hình tổng quan về các giao thức định tuyến đang chạy trên thiết bị, bao gồm cấu hình OSPF.

- `show ip ospf neighbor`: Liệt kê các hàng xóm OSPF (các thiết bị khác mà thiết bị của bạn đang trao đổi thông tin định tuyến OSPF với) cùng với các thông tin liên quan như địa chỉ IP, state và router ID.

- `show ip ospf interface`: Hiển thị cấu hình OSPF trên từng giao diện, bao gồm trạng thái của giao diện, cost, và các thông số OSPF khác.

- `show ip ospf database`: Hiển thị nội dung của cơ sở dữ liệu OSPF, bao gồm các mạng, router và link-state advertisements (LSAs).

- `show ip ospf`: Hiển thị thông tin tổng quan về OSPF, bao gồm OSPF process ID, router ID, area ID và các thông số OSPF khác.

- `show ip route ospf`: Hiển thị bảng định tuyến OSPF, cho biết các đường đi OSPF hiện đang được thiết lập trên thiết bị.