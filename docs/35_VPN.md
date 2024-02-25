# Virtual Private Network (VPN)

## Khái niệm và mục đích

- `Mạng riêng ảo (VPN)` là một công nghệ cho phép bạn tạo ra một kết nối mạng riêng tư và an toàn qua một mạng công cộng như internet. Khi bạn kết nối vào một VPN, dữ liệu của bạn được mã hóa và đóng gói vào gói tin được gửi thông qua một kết nối an toàn đến một máy chủ VPN, sau đó đi ra internet. Điều này giúp che giấu địa chỉ IP thực sự của bạn và bảo vệ thông tin truyền qua mạng, làm cho nó trở nên khó khăn hơn cho bất kỳ ai đang nghe trộm hoặc theo dõi dữ liệu của bạn.

- Mục đích sử dụng VPN

	+ Bảo vệ sự riêng tư trực tuyến: Bằng cách ẩn địa chỉ IP của bạn và mã hóa dữ liệu, VPN giúp ngăn chặn việc theo dõi và thu thập thông tin cá nhân của bạn khi bạn duyệt web hoặc sử dụng dịch vụ trực tuyến.

	+ Truy cập vào nội dung bị hạn chế: VPN cho phép bạn truy cập vào nội dung trực tuyến bị chặn hoặc hạn chế theo địa lý bằng cách kết nối đến máy chủ VPN nằm ở quốc gia có quyền truy cập vào nội dung đó.

	+ Bảo vệ khi kết nối từ mạng công cộng: Khi bạn kết nối từ một mạng Wi-Fi công cộng, VPN giúp bảo vệ thông tin của bạn khỏi các mối đe dọa như tin tặc và phần mềm đánh cắp thông tin.

## Phân loại VPN

1. `Remote Access VPN (VPN Truy cập từ xa)`: Loại VPN này cho phép người dùng kết nối vào mạng riêng của tổ chức từ xa thông qua internet. Nó cho phép nhân viên hoặc người dùng từ xa truy cập vào tài nguyên mạng nội bộ như tệp chia sẻ, ứng dụng và dịch vụ mạng một cách an toàn.

2. `Site-to-Site VPN (VPN từ trang này đến trang khác)`: Loại VPN này cho phép kết nối giữa hai hoặc nhiều mạng riêng của các địa điểm vật lý khác nhau thông qua internet. Điều này cho phép các văn phòng hoặc chi nhánh của cùng một tổ chức kết nối và chia sẻ tài nguyên mạng một cách an toàn.

3. `Client-to-Site VPN (VPN từ máy khách đến trang)`: Tương tự như Remote Access VPN, loại VPN này cho phép các máy khách cá nhân kết nối vào mạng riêng của tổ chức thông qua internet.

4. `Peer-to-Peer VPN (VPN Ngang hàng)`: Loại VPN này cho phép các máy tính hoặc thiết bị kết nối trực tiếp với nhau mà không cần thông qua một máy chủ trung gian. Điều này thường được sử dụng trong các mô hình mạng ngang hàng, nơi các thiết bị cần kết nối trực tiếp với nhau để chia sẻ tài nguyên hoặc dữ liệu mà không cần sự trung gian của một máy chủ.

5. `SSL/TLS VPN (VPN dựa trên SSL/TLS)`: Loại VPN này sử dụng giao thức SSL (Secure Sockets Layer) hoặc TLS (Transport Layer Security) để thiết lập kết nối an toàn giữa người dùng và mạng VPN. Thường được sử dụng cho việc truy cập từ xa vào ứng dụng web hoặc portal dựa trên trình duyệt.

## Các loại kênh ảo

1. `PVC (Permanent Virtual Circuit)`

- PVC là một kênh ảo được thiết lập trước và cố định giữa hai điểm trong mạng.

- Kênh PVC không thay đổi trong quá trình sử dụng và được xác định trước bằng các tham số như địa chỉ và thông tin định tuyến.

- PVC thường được sử dụng trong mạng ATM (Asynchronous Transfer Mode) và Frame Relay để tạo ra các kết nối ổn định và đáng tin cậy giữa các điểm trong mạng.

2. `SVC (Switched Virtual Circuit)`

- SVC là một kênh ảo được tạo ra và xác định theo yêu cầu khi cần thiết và được loại bỏ khi không cần thiết nữa.

- Khi một thiết bị muốn gửi dữ liệu đến một đích, nó có thể yêu cầu tạo ra một SVC từ điểm xuất phát đến điểm đích thông qua mạng.

- SVC thường được sử dụng trong mạng ATM để cung cấp khả năng động và linh hoạt trong việc quản lý tài nguyên mạng.

## Giao thức GRE

1. Khái niệm

- Giao thức GRE (Generic Routing Encapsulation) là một giao thức được sử dụng trong mạng máy tính để đóng gói và truyền dữ liệu qua mạng công cộng, chẳng hạn như internet. 

- GRE cho phép tạo ra các kênh ảo giữa các thiết bị mạng, cung cấp khả năng đóng gói các gói tin của một giao thức mạng vào bên trong gói tin GRE và gửi chúng qua mạng công cộng.

2. Đặc điểm và tính năng

- `Đóng gói dữ liệu`: GRE đóng gói dữ liệu của một giao thức mạng vào trong một gói tin GRE. Điều này cho phép dữ liệu từ một mạng có thể được truyền qua một mạng công cộng hoặc không tin cậy mà không lo lắng về việc bị mất hoặc bị sửa đổi.

- `Tính linh hoạt`: GRE là một giao thức linh hoạt, cho phép truyền nhiều loại dữ liệu khác nhau bên trong các gói tin GRE, bao gồm các giao thức mạng như IP, IPv6, và các giao thức mạng khác.

- `Hỗ trợ mạng ảo`: GRE cho phép tạo ra các kênh ảo giữa các thiết bị mạng, cung cấp khả năng mở rộng mạng và kết nối các mạng với nhau một cách linh hoạt.

- `Bảo mật`: Mặc dù GRE không cung cấp các tính năng bảo mật mạnh mẽ như mã hóa dữ liệu, nhưng nó có thể được kết hợp với các giao thức bảo mật khác như IPsec để cung cấp tính an toàn cho dữ liệu.

3. Cấu trúc GRE

- `Header GRE`: Đây là phần đầu tiên của gói tin GRE và chứa các trường thông tin quan trọng cho việc xác định các thông tin cần thiết để định tuyến và xử lý gói tin. Các trường quan trọng trong header GRE bao gồm:

	+ `Version (phiên bản)`: Xác định phiên bản của giao thức GRE.

	+ `Protocol Type`: Xác định giao thức mạng được đóng gói bên trong gói tin GRE (ví dụ: IP, IPv6).

	+ `Key`: Một số trường không bắt buộc, thường được sử dụng cho mục đích bảo mật.

	+ `Sequence Number`: Số thứ tự của gói tin GRE, thường được sử dụng trong các trường hợp cần thiết.

- `Optional GRE Header Fields (trường tiêu chí của GRE)`: Có thể bao gồm các trường bổ sung như Checksum hoặc Routing Information, nhưng không bắt buộc.

- `Payload (Dữ liệu Payload)`: Đây là phần dữ liệu thực sự được đóng gói bên trong gói tin GRE. Payload này có thể là bất kỳ dữ liệu nào của giao thức mạng (IP, IPv6, hoặc giao thức khác) mà gói tin GRE đang chuyển.

==> Gói tin GRE cho phép đóng gói các gói tin của một giao thức mạng bên trong gói tin GRE và truyền chúng qua mạng công cộng hoặc không đáng tin cậy mà không lo lắng về việc bị mất hoặc bị sửa đổi. Điều này rất hữu ích trong các tình huống như triển khai các mạng riêng ảo (VPN) hoặc kết nối các mạng qua mạng công cộng.

4. Cấu hình và ví dụ

Ta sẽ cấu hình một kết nối VPN sử dụng giao thức GRE trên hai thiết bị router trong một mạng

+ Trên Router1:

```sh
R1(config)# interface Tunnel0
R1(config-if)# no shut
R1(config-if)# ip address 10.1.1.1 255.255.255.0  // Đặt địa chỉ IP cho tunnel interface
R1(config-if)# tunnel source 192.168.1.1          // Xác định địa chỉ IP của giao diện ra mạng công cộng (public interface)
R1(config-if)# tunnel destination 203.0.113.1     // Xác định địa chỉ IP của router đích
R1(config-if)# tunnel mode gre ip                  // Xác định giao thức cho tunnel là GRE và IP
```
+ Trên Router2:

```sh
R2(config)#interface Tunnel0
R2(config-if)# no shut
R2(config-if)# ip address 10.1.1.2 255.255.255.0  // Đặt địa chỉ IP cho tunnel interface
R2(config-if)# tunnel source 203.0.113.1         // Xác định địa chỉ IP của giao diện ra mạng công cộng (public interface)
R2(config-if)# tunnel destination 192.168.1.1    // Xác định địa chỉ IP của router đích
R2(config-if)# tunnel mode gre ip                  // Xác định giao thức cho tunnel là GRE và IP
```

+ Trong ví dụ này:

	+ Hai router sử dụng giao thức GRE để tạo một kết nối tunnel giữa chúng.

	+ Tunnel được cấu hình với địa chỉ IP trên mỗi đầu là 10.1.1.1 (Router1) và 10.1.1.2 (Router2).

	+ Địa chỉ IP của giao diện ra mạng công cộng (public interface) được sử dụng như là nguồn (source) và điểm đích (destination) của tunnel trên mỗi router.

	+ Tunnel mode được xác định là GRE và IP.

## Kiểm tra cấu hình

1. Hiển thị cấu hình của interface Tunnel

```sh
show interface tunnel <number>
```

2. Hiển thị thông tin về kết nối tunnel GRE

```sh
show interface tunnel <number> tunnel
```

3. Hiển thị các routes được học thông qua kết nối tunnel

```sh
show ip route
```

4. Kiểm tra trạng thái của kết nối tunnel

```sh
show interface tunnel <number> status
```

5. Kiểm tra lưu lượng thông qua kết nối tunnel

```sh
show interface tunnel <number> | include <input rate/output rate>
```