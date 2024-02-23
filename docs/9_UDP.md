# UDP (User Datagram Protocol)

- Đây là một trong hai giao thức chính được sử dụng trong Internet Protocol Suite, cùng với TCP (Transmission Control Protocol)

## Mục đích 

- UDP được thiết kế để cung cấp một cách nhanh chóng và hiệu quả để truyền dữ liệu qua mạng. Nó không có các tính năng như kiểm soát lỗi, kiểm soát luồng và tái tạo dữ liệu một cách đảm bảo như TCP.

## Đặc điểm chính:

1. `Không đảm bảo tin cậy`: UDP không đảm bảo việc gửi và nhận dữ liệu một cách đảm bảo như TCP. Nó không có cơ chế kiểm soát lỗi, điều này có nghĩa là các gói tin có thể bị mất hoặc bị trùng lặp trong quá trình truyền.

2. `Không có kết nối`: Khác với TCP, UDP không thiết lập kết nối trước khi truyền dữ liệu. Điều này có nghĩa là không có quá trình thiết lập kết nối (handshake) như TCP, và không có trạng thái kết nối được duy trì trên cả hai bên.

3. `Tốc độ`: Do không có các cơ chế kiểm soát và xác nhận như TCP, UDP có thể truyền dữ liệu nhanh hơn trong một số trường hợp.

4. `Đơn giản`: UDP là một giao thức đơn giản và nhẹ, thường được sử dụng trong các ứng dụng yêu cầu tốc độ cao và có thể chấp nhận mất mát dữ liệu như video streaming và trò chơi trực tuyến.

5. `Ứng dụng phổ biến`: UDP thường được sử dụng trong các ứng dụng yêu cầu tốc độ cao và không nhất thiết phải đảm bảo tin cậy, bao gồm video streaming, trò chơi trực tuyến, VoIP (Voice over IP), DNS (Domain Name System), và SNMP (Simple Network Management Protocol).

## Tiêu đề UDP

1. Tiêu đề của giao thức UDP có kích thước cố định là 8 byte. Không giống như TCP, UDP không có các trường tùy chọn mở rộng, do đó kích thước của tiêu đề là cố định và không thay đổi.

2. Tiêu đề UDP bao gồm các trường sau:

- Tổng kích thước của tiêu đề UDP là 8 byte.

	+ `Port nguồn (Source Port)`: 2 byte.

	+ `Port đích (Destination Port)`: 2 byte.

	+ `Độ dài (Length)`: 2 byte.

	+ `Checksum`: 2 byte.
	
- UDP không có các trường như số thứ tự, số thứ tự xác nhận, cờ, cửa sổ hay các tùy chọn như TCP. Do đó, tiêu đề của nó đơn giản và nhẹ nhàng hơn so với tiêu đề của TCP.

- UDP cung cấp một lựa chọn linh hoạt cho việc truyền dữ liệu qua mạng trong những trường hợp mà tốc độ và hiệu suất được ưu tiên hơn so với độ tin cậy và đảm bảo.