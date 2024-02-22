# BGP (Border Gateway Protocol)

1. Một số khái niệm cơ bản

- BGP (Border Gateway Protocol) là một giao thức định tuyến được sử dụng để trao đổi thông tin định tuyến giữa các mạng lớn trên internet.

- AS (Autonomous System): Một hệ thống tự trị là một tập hợp các mạng và thiết bị định tuyến được quản lý bởi một tổ chức duy nhất và hoạt động dưới một quy tắc chung. Mỗi AS được gán một số định danh duy nhất trên toàn thế giới.

- EBGP (External BGP): BGP diễn ra giữa các AS khác nhau, được gọi là EBGP. Trong trường hợp này, các máy chủ BGP nằm ở các tổ chức hoặc mạng khác nhau.

- IBGP (Internal BGP): BGP diễn ra giữa các máy chủ BGP trong cùng một AS, được gọi là IBGP.

- BGP Peering: Quá trình thiết lập kết nối giữa hai hoặc nhiều máy chủ BGP để trao đổi thông tin định tuyến.

- BGP Route: Một bản ghi trong bảng định tuyến BGP, bao gồm địa chỉ IP mục tiêu, các thuộc tính và thông tin đường đi.

- BGP Attributes: Thuộc tính được sử dụng để quyết định việc chọn đường đi trong BGP. Các thuộc tính này bao gồm AS Path, Next Hop, Local Preference, Weight, và nhiều thuộc tính khác.

- AS Path: Là một trong các thuộc tính quan trọng nhất trong BGP, xác định các AS mà một tuyến đường đã đi qua.

- Next Hop: Địa chỉ IP của router tiếp theo mà dữ liệu được chuyển đến trên đường đi đến mục tiêu.

- Prefix: Địa chỉ IP và subnet mask của một mạng được định tuyến.

- BGP Route Advertisement: Hành động thông báo các đường đi BGP tới các máy chủ BGP khác.

- BGP Route Selection: Quá trình lựa chọn đường đi tốt nhất dựa trên các thuộc tính và tiêu chí xác định.

- BGP Community: Một cách để gán một nhóm các tuyến đường cụ thể cho một tên gọi hoặc nhãn để điều chỉnh hành vi định tuyến.

- BGP Confederation: Một phương pháp để chia nhỏ một AS lớn thành các phần nhỏ hơn để quản lý dễ dàng hơn.

- BGP Route Reflectors: Các máy chủ được cấu hình để phản ánh thông tin định tuyến giữa các peer trong cùng một AS, giúp giảm bớt khối lượng thông tin định tuyến.

2. Cấu hình BGP

- Cấu hình cơ bản

```sh

router bgp <AS_number>	//Bắt đầu quá trình BGP
no synchronization	//Tắt đồng bộ hóa
network <network_address> mask <subnet_mask>	//Chỉ định network mà router sẽ quảng bá thông qua BGP
neighbor <IP_address> remote-as <remote_AS_number>	//Thiết lập kết nối với neighbor

```

- Sử dụng loopback làm địa chỉ nguồn cho BGP

```sh
neighbor <IP_address> update-source loopback<number>	//Sử dụng loopback làm địa chỉ nguồn cho BGP
```
- Chỉ định Next Hop Self

```sh
neighbor <IP_address> next-hop-self		//Chỉ định Next Hop Self
```

- Chỉ định BGP Community

```sh
neighbor <IP_address> send-community	//Cho phép router gửi thông tin BGP Community cho neighbor
```

3. Lệnh kiểm tra cấu hình

- Hiển thị chi tiết cấu hình BGP

```sh 
show ip bgp
```
- Kiểm tra thông tin về một neighbor cụ thể

```sh
show ip bgp neighbor <neighbor_IP_address>
```

- Hiển thị tóm tắt cấu hình BGP

```sh
show running-config | section router bgp
```

- Hiển thị tóm tắt các neighbor BGP

```sh
show ip bgp summary
```

- Kiểm tra thông tin về các prefix cụ thể

```sh
show ip bgp <prefix>
```