# ACL (Access Control List)

## Một số khái niệm, đặc điểm 

- Access Control List (ACL) là một công cụ quản lý truy cập được sử dụng trong các thiết bị mạng như router và firewall để kiểm soát lưu lượng truy cập vào hoặc ra khỏi mạng.

- ACL là một danh sách các quy tắc được áp dụng tuần tự từ trên xuống dưới, và mỗi quy tắc định rõ các điều kiện và hành động áp dụng cho các gói tin dữ liệu.

1. Các loại ACL 

- Có 2 loại chính của ACL là:  `Standard ACL` và `Extended ACL`

	- `Standard ACL`: Kiểm soát truy cập dựa trên địa chỉ IP nguồn hoặc đích, thường được sử dụng ở mức độ đơn giản và ít phức tạp.

	- `Extended ACL`: Kiểm soát truy cập dựa trên nhiều yếu tố như địa chỉ IP nguồn và đích, cổng TCP/UDP, giao thức, v.v., cung cấp khả năng kiểm soát linh hoạt hơn.

2. Cách áp dụng: ACL được áp dụng tại cổng (interface) của router hoặc firewall, quyết định xem gói tin dữ liệu sẽ được chấp nhận, từ chối hoặc chuyển hướng.

3. Cấu trúc quy tắc ACL:

- Mỗi quy tắc ACL bao gồm một số điều kiện (hoặc điều kiện phủ định) và một hành động.

	- `Điều kiện`: Xác định các yếu tố để so sánh với các gói tin dữ liệu, chẳng hạn như địa chỉ IP nguồn/đích, cổng, giao thức, v.v.

	- `Hành động`: Xác định hành động sẽ được thực hiện nếu gói tin khớp với điều kiện, chẳng hạn như chấp nhận (permit), từ chối (deny) hoặc chuyển hướng (đối với firewall).

4. Thứ tự ưu tiên: Quy tắc trong ACL được áp dụng tuần tự từ trên xuống dưới, vì vậy thứ tự của chúng rất quan trọng. Khi một gói tin khớp với một quy tắc, các quy tắc sau không được xem xét nữa (nếu không có ánh xạ ngoại lệ được cấu hình).

5. Mục đích sử dụng: ACL được sử dụng để cung cấp bảo mật mạng, kiểm soát lưu lượng truy cập, triển khai chính sách và quản lý tài nguyên mạng.

## Cấu hình ACL

1. Tạo ACL

```sh
ip access-list <number> {standard | extended}
```

2. Thêm quy tắc vào ACL

```sh
permit|deny [source_address] [wildcard_mask] [destination_address] [wildcard_mask] [protocol] [operator port]
```

3. Áp dụng ACL

```sh
interface <interface>
ip access-group {<number> | <name>} {in | out}
```
4. Ví dụ

Giả sử bạn muốn tạo một ACL để từ chối lưu lượng truy cập từ một mạng con cụ thể vào một cổng cụ thể của router.

```sh
Router(config)# ip access-list extended BLOCK_TRAFFIC
Router(config-ext-nacl)# deny ip 192.168.1.0 0.0.0.255 any
Router(config)# interface G0/0
Router(config-if)# ip access-group BLOCK_TRAFFIC in
```
> Trong đó:

- `deny`: Từ chối các gói tin có địa chỉ nguồn từ mạng con 192.168.1.0/24 và đích là bất kỳ nơi nào.

- `ip`: Xác định loại gói tin là IPv4.

- `192.168.1.0 0.0.0.255`: Địa chỉ mạng và mask của mạng con cần từ chối.

- `any`: Áp dụng cho tất cả các địa chỉ đích.

> Điều này sẽ từ chối tất cả lưu lượng truy cập từ mạng con 192.168.1.0/24 vào cổng vào của router.

## Lệnh kiểm tra cấu hình

1. `show ip access-lists`: Lệnh này sẽ hiển thị danh sách tất cả các ACL cùng với các quy tắc được định nghĩa bên trong chúng, bao gồm số hiệu ACL, loại ACL (standard hoặc extended), và chi tiết các quy tắc bao gồm điều kiện và hành động.

2. `show access-lists`: Lệnh này cũng sẽ hiển thị danh sách tất cả các ACL cùng với các quy tắc được định nghĩa bên trong chúng, tương tự như `show ip access-lists`. Tùy thuộc vào phiên bản IOS cụ thể, bạn có thể cần sử dụng lệnh này thay vì `show ip access-lists`.

3. Ví dụ: Bạn tạo một ACL như ví dụ mục 4 ở trên và muốn kiểm tra cấu hình của nó, bạn có thể sử dụng lệnh:

```sh
Router# show ip access-lists BLOCK_TRAFFIC
```
hoặc

```sh
Router# show access-lists BLOCK_TRAFFIC
```


