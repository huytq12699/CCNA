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
access-list <number> [permit | deny] [IP source_address] [wildcard_mask]

or 

ip access-list standard <name> [permit | deny] [IP source_address] [wildcard_mask]
```

2. Thêm quy tắc vào ACL

```sh
permit|deny [source_address] [wildcard_mask] [destination_address] [wildcard_mask] [protocol] [port]
```

3. Áp dụng ACL

```sh
interface <interface>
ip access-group {<number> | <name>} {in | out}
```
4. Ví dụ

- Cấu hình Standard Access-list 

```sh
Router(config)#access-list 1 deny 172.16.0.0 0.0.255.255 
Router(config)#access-list 1 permit any 
Router(config)#interface fastethernet 0/0 
Router(config-in)#ip access-group in 
```

- Cấu hình Extended Access-list

```sh
Router(config)#access-list 101 deny tcp 172.16.0.0 0.0.255.255 host 192.168.1.1 eq telnet 
Router(config)#access-list 101 deny tcp 172.16.0.0 0.0.255.255 host 192.168.1.2 eq ftp 
Router(config)#access-list 101 permit any any 
Router(config)#interface fastethernet 0/0 
Router(config-int)#ip access-group out 
```

- Cấu hình named ACL thay cho các số hiệu

```sh
Router(config)#ip access-list extended <name> (tên của access-list) 
Router(config-ext-nacl)#permit tcp any host 192.168.1.3 eq telnet 
Router(config)#interface fastethernet 0/0 
Router(config-int)#ip access-group <name> out 
```

5. Xóa ACL

```sh
Router(config)# no ip access-list id
```

6. Lưu ý

- Mặc định của tất cả Access-list là `deny all`, vì vậy trong tất cả các access-list tối thiểu phải có `1 lệnh permit`. Nếu trong access-list có cả permit và deny thì nên để các dòng lệnh permit bên trên.

- Về hướng của access-list (In/Out) khi áp dụng vào cổng có thể hiểu đơn giản là: `In` là từ host, `Out` là tới host 
hay `In` vào trong Router, còn `Out` là ra khỏi Router.

- Đối với `IN router` kiểm tra gói tin trước khi nó được đưa tới bảng xử lý. Đối với `OUT`, router kiểm tra gói tin sau khi nó vào bảng xử lý. 

- Wildcard mask được tính bằng công thức:

```sh
Wildcard_mask = 255.255.255.255 – Subnet mask (Áp dụng cho cả Classful và Classless addreess) 
--> 0.0.0.0 255.255.255.255 = any. 
--> Ip address 0.0.0.0 = host ip address (chỉ định từng host một ) 
```
## Lệnh kiểm tra cấu hình

1. `show ip access-lists`: Lệnh này sẽ hiển thị danh sách tất cả các ACL cùng với các quy tắc được định nghĩa bên trong chúng, bao gồm số hiệu ACL, loại ACL (standard hoặc extended), và chi tiết các quy tắc bao gồm điều kiện và hành động.

2. `show access-lists`: Lệnh này cũng sẽ hiển thị danh sách tất cả các ACL cùng với các quy tắc được định nghĩa bên trong chúng, tương tự như `show ip access-lists`. Tùy thuộc vào phiên bản IOS cụ thể, bạn có thể cần sử dụng lệnh này thay vì `show ip access-lists`.



