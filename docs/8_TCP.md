# TCP (Transmission Control Protocol)

1. Mục đích

- TCP là một trong hai giao thức chính được sử dụng trong Internet Protocol Suite (cùng với giao thức UDP). Nó được thiết kế để cung cấp một kênh truyền tin cậy và có đặc tính kết nối cho việc truyền dữ liệu qua mạng.

2. Đặc điểm chính

- Tin cậy: TCP sử dụng cơ chế ACK (Acknowledgement) để đảm bảo rằng dữ liệu đã được gửi đến đích một cách chính xác và đầy đủ. Nếu một gói tin bị mất hoặc bị hỏng, nó sẽ được gửi lại.

- Kết nối: TCP thiết lập kết nối giữa máy gửi và máy nhận trước khi truyền dữ liệu. Quá trình này bao gồm ba bước: thiết lập kết nối (handshake), truyền dữ liệu và đóng kết nối.

- Dòng truyền: TCP sử dụng cơ chế cửa sổ trượt (sliding window) để quản lý dòng truyền dữ liệu, điều này cho phép nó điều chỉnh tốc độ truyền dữ liệu tùy thuộc vào điều kiện mạng.

- Ghi nhận thứ tự: TCP đảm bảo rằng các gói tin được gửi từ máy gửi đến máy nhận theo đúng thứ tự được gửi.

3. Tiêu đề TCP 

- Có kích thước cố định là `20 byte` khi không tính các tùy chọn mở rộng. Tùy chọn mở rộng có thể làm tăng kích thước của tiêu đề TCP lên đến tối đa là `60 byte`.

- Tiêu đề TCP bao gồm các trường sau:

	+ `Port nguồn (Source Port)`: 2 byte

	+ `Port đích (Destination Port)`: 2 byte

	+ `Số thứ tự (Sequence Number)`: 4 byte

	+ `Số thứ tự xác nhận (Acknowledgment Number)`: 4 byte

	+ `Độ dài tiêu đề (Header Length)`: 4 bit, tối đa là 15 dấu hiệu bit (tương đương với 60 byte)

	+ `Cờ (Flags)`: Có 6 cờ, mỗi cờ chiếm 1 bit

	+ `Cửa sổ (Window)`: 2 byte

	+ `Checksum`: 2 byte

	+ `Urgent Pointer`: 2 byte

	+ `Tùy chọn (Options)`: Nếu có, kích thước có thể biến đổi từ 0 đến 40 byte

	+ Tổng kích thước của tiêu đề TCP (không tính các tùy chọn mở rộng) là 20 byte. Tuy nhiên, khi có tùy chọn mở rộng, kích thước tiêu đề TCP có thể lớn hơn 20 byte.

4. Cổng và Số thứ tự:

- Mỗi kết nối TCP được xác định bằng cặp địa chỉ IP đích và cổng đích. Các cổng TCP được sử dụng để xác định ứng dụng hoặc dịch vụ cụ thể mà dữ liệu được gửi đến. Số thứ tự được sử dụng để xác định vị trí của mỗi byte dữ liệu trong luồng dữ liệu.

- Một số ứng dụng và dịch vụ tương ứng với các Port đích

| Port đích | Ứng dụng/Dịch vụ |
| ----------|-------- |
| 80 | Web |
| 443 | HTTPS |
| 25| SMTP |
| 53 | DNS |
| 110 | POP |
| 20/21 | FTP |
| 23 | Telnet |

5. Bảo mật

- TCP không có tính năng bảo mật tích hợp. Tuy nhiên, nó thường được kết hợp với các giao thức bảo mật như SSL/TLS để tạo ra kết nối an toàn.

6. Ứng dụng phổ biến

- TCP được sử dụng rộng rãi trong các ứng dụng như truyền tệp qua mạng, duyệt web, email (qua giao thức SMTP, POP3, IMAP), truyền file qua FTP, và nhiều ứng dụng mạng khác.
