# Point-to-Point (P2P)

## Tìm hiểu chung

1. Khái niệm

- `Point-to-Point (P2P)` là một khái niệm trong lĩnh vực mạng máy tính và truyền thông, chỉ một loại kết nối trực tiếp giữa hai thiết bị hoặc nút trong một mạng. 

- Trong P2P, dữ liệu được truyền trực tiếp từ nguồn tới đích mà không thông qua bất kỳ thiết bị trung gian nào khác. Điều này khác biệt so với kiểu truyền thông khác như multicast (một nguồn gửi đến nhiều điểm) hoặc broadcast (một nguồn gửi đến tất cả các điểm).

- Các ví dụ phổ biến về P2P bao gồm:

	+ `Kết nối trực tiếp giữa hai máy tính`: Trong mạng máy tính, hai máy tính có thể thiết lập một kết nối P2P để trao đổi dữ liệu trực tiếp mà không cần qua máy chủ trung gian.

	+ `Kết nối giữa hai điểm cuối trong mạng VPN`: Khi sử dụng mạng riêng ảo (VPN), kết nối P2P được sử dụng giữa máy tính của người dùng và máy chủ VPN.

	+ `Kết nối giữa hai điểm trong hệ thống điều khiển hoặc tự động hóa`: Trong các ứng dụng công nghiệp, P2P thường được sử dụng để kết nối các thiết bị và máy tính điều khiển với nhau một cách trực tiếp.

2. Ưu và nhược điểm

- Ưu điểm: P2P có nhiều ưu điểm như đơn giản, tiết kiệm chi phí và độ trễ thấp do loại bỏ sự phụ thuộc vào các thiết bị trung gian. 

- Nhược điểm: Hạn chế trong việc mở rộng lên quy mô lớn do các vấn đề về quản lý và bảo trì khi số lượng điểm kết nối tăng lên.

## Các giao thức trong P2P

1. `LCP (Link Control Protocol)`:

- LCP là một phần của PPP được sử dụng để thiết lập, cấu hình và kiểm soát các kết nối PPP.

- Nhiệm vụ chính của LCP là đàm phán các tham số kết nối như định dạng frame, kiểu mã hóa, kiểu kiểm tra lỗi, cấu hình IP, và các tham số liên quan khác.

- LCP cũng kiểm tra tính hợp lệ của các tham số kết nối và thực hiện các hoạt động để duy trì kết nối như kiểm tra liên lạc với đối tác.

2. `NCP (Network Control Protocol)`:

- NCP là một tầng phía trên của PPP được sử dụng để thiết lập và cấu hình các giao thức mạng khác như IP, IPX (Internetwork Packet Exchange), và làm việc với các dịch vụ mạng như PPPoE (PPP over Ethernet).

- Mỗi loại dịch vụ mạng cần sử dụng một phiên bản cụ thể của NCP. Ví dụ, để sử dụng giao thức IP trên kết nối PPP, NCP IP sẽ được sử dụng để thiết lập và cấu hình các tham số IP như địa chỉ IP, subnet mask, và default gateway.

## Cấu hình P2P

1. Cấu hình P2P Multilink: cấu hình 2 Router sử dụng kết nối P2P Multilink

- Trên Router1: 

	+ Cấu hình giao diện đối tác cho mỗi kết nối PPP và tham gia vào nhóm Multilink

```sh
	Router1(config)# interface Serial0/0/0
	Router1(config-if)# encapsulation ppp
	Router1(config-if)# ppp multilink
	Router1(config-if)# ppp multilink group 1
	Router1(config-if)# no shutdown

	Router1(config)# interface Serial0/0/1
	Router1(config-if)# encapsulation ppp
	Router1(config-if)# ppp multilink
	Router1(config-if)# ppp multilink group 1
	Router1(config-if)# no shutdown
```
   + Tạo một giao diện Multilink và liên kết các giao diện đối tác với nó

```sh
	Router1(config)# interface Multilink1
	Router1(config-if)# ip address 10.0.0.1 255.255.255.0
	Router1(config-if)# ppp multilink
	Router1(config-if)# ppp multilink group 1
	Router1(config-if)# no shutdown
	Router1(config-if)# exit
```

- Trên Router2:
	
	+ Cấu hình giao diện đối tác cho mỗi kết nối PPP và tham gia vào nhóm Multilink

```sh
	Router2(config)# interface Serial0/0/0
	Router2(config-if)# encapsulation ppp
	Router2(config-if)# ppp multilink
	Router2(config-if)# ppp multilink group 1
	Router2(config-if)# no shutdown

	Router2(config)# interface Serial0/0/1
	Router2(config-if)# encapsulation ppp
	Router2(config-if)# ppp multilink
	Router2(config-if)# ppp multilink group 1
	Router2(config-if)# no shutdown
```
   + Tạo một giao diện Multilink và liên kết các giao diện đối tác với nó

```sh
	Router2(config)# interface Multilink1
	Router2(config-if)# ip address 10.0.0.2 255.255.255.0
	Router2(config-if)# ppp multilink
	Router2(config-if)# ppp multilink group 1
	Router2(config-if)# no shutdown
	Router2(config-if)# exit
```

2. Cấu hình P2P authentication

- Sử dụng Password Authentication Protocol (PAP)

```sh
Router(config)# interface Serial0/0/0
Router(config-if)# encapsulation ppp
Router(config-if)# ppp authentication pap
Router(config-if)# username <username> password <password>
Router(config-if)# no shutdown
```

- Sử dụng Challenge Handshake Authentication Protocol (CHAP)

```sh
Router(config)# interface Serial0/0/0
Router(config-if)# encapsulation ppp
Router(config-if)# ppp authentication chap
Router(config-if)# username <username> password <password>
Router(config-if)# no shutdown
```

## Kiểm tra cấu hình

1. Kiểm tra trạng thái kết nối PPP:

```sh
Router# show ppp multilink
```

2. Kiểm tra trạng thái xác thực PPP:

```sh
Router# show ppp authentication
```

3. Kiểm tra cấu hình giao diện PPP

```sh
Router# show interface <interface_id>
```
