# So sánh 

| Tiêu chí | VRRP |	HSRP |
| -------- | ----- | ----- |
| Mục đích | Cung cấp khả năng sao lưu cho các thiết bị mạng, giảm thiểu sự gián đoạn trong trường hợp một thiết bị chính thất bại. | Cung cấp khả năng sao lưu cho các thiết bị mạng, giảm thiểu sự gián đoạn trong trường hợp một thiết bị chính thất bại. |
| Loại giao thức |	Tiêu chuẩn của IETF (RFC 3768) |	Cisco Proprietary |
| Số Router | Hỗ trợ nhiều hơn 2 Router | Thường được triển khai tối đa 2 Router |
| Hoạt động |	Một thiết bị được chọn làm "thiết bị chính" (master), các thiết bị khác hoạt động dự phòng (backup). Nếu thiết bị chính thất bại, thiết bị dự phòng sẽ tiếp tục chịu trách nhiệm. |	Tương tự như VRRP, một thiết bị được chọn làm "thiết bị chính" (active), các thiết bị khác là "thiết bị dự phòng" (standby). Nếu thiết bị chính thất bại, thiết bị dự phòng sẽ tiếp tục chịu trách nhiệm. |
| Chức năng | Hỗ trợ tính toán IP checksum. | Hỗ trợ thiết lập IP phụ. |
| Cấu trúc địa chỉ |	IPv4 và IPv6 |	Chủ yếu IPv4 |
| Số lượng thiết bị	| Tối đa 255 thiết bị | Tối đa 255 thiết bị |
| Metric |	Không |	Có |
| Tracking |	Có	| Có |
| Thời gian chuyển đổi |	<1 giây | 	<1 giây |
| Tương thích |	Tương thích với các thiết bị từ nhiều nhà cung cấp. |	Chủ yếu được triển khai trên thiết bị Cisco. |
| Độ phổ biến | Phổ biến trong môi trường kinh doanh và mạng lớn. | Phổ biến trong các mạng sử dụng thiết bị Cisco. |

