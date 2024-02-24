# Spanning-tree Protocol (STP)

## Một số khái niệm cơ bản

- Giao thức Spanning Tree Protocol (STP) là một trong những giao thức quan trọng trong mạng máy tính, được sử dụng để ngăn chặn việc xảy ra các vòng lặp trong mạng chuyển mạch Ethernet. Khi một mạng có nhiều đường kết nối giữa các switch, có thể xảy ra các vòng lặp, dẫn đến hiện tượng broadcast storm và gây tắc nghẽn mạng.

- Là giao thức mặc định, nằm trong chuẩn IEEE 802.1D

- `Root Bridge`: Đây là switch có ID root bridge thấp nhất, là trung tâm của cấu trúc cây mà STP tạo ra. Tất cả các switch trong mạng sẽ tính toán các đường đi tới root bridge.

- `Bridge ID`: Định danh duy nhất của mỗi switch trong mạng. Bridge ID bao gồm một địa chỉ MAC và một priority value.

- `Port State`: Mỗi cổng trên switch có thể ở một trong các trạng thái sau:

	+ `Blocking`: Cổng không tham gia gửi hoặc nhận dữ liệu, nhưng vẫn lắng nghe các gói tin BPDU để thực hiện quyết định về topology.

	+ `Listening`: Cổng đang lắng nghe BPDU, chuẩn bị chuyển từ Blocking sang Learning.

	+ `Learning`: Cổng đang lắng nghe BPDU và học MAC address của các thiết bị gắn liền với nó, chuẩn bị chuyển sang Forwarding.

	+ `Forwarding`: Cổng đã học được thông tin và tham gia gửi và nhận dữ liệu.

- `BPDU (Bridge Protocol Data Unit)`: Là các gói tin chuyển tiếp giữa các switch để thực hiện việc tính toán topology và kiểm soát STP.

- `Convergence`: Là quá trình mà mạng hội tụ vào một topology ổn định sau khi có sự thay đổi trong cấu trúc mạng.

## Cách hoạt động

1. `Chọn Root Bridge`: Ban đầu, mỗi switch trong mạng xác định chính nó và các switch khác thông qua gửi các gói tin BPDU (Bridge Protocol Data Unit). BPDU chứa thông tin về Bridge ID (bao gồm MAC address của switch và priority value). Các switch so sánh Bridge ID của chính mình với các BPDU nhận được để xác định switch có Bridge ID nhỏ nhất sẽ là Root Bridge.

2. `Chọn Root Port`: Mỗi switch xác định cổng nào kết nối trực tiếp với Root Bridge và đặt cổng đó là Root Port. Root Port là cổng có đường đi ngắn nhất đến Root Bridge. Nếu có nhiều đường đi có cùng chiều dài, switch sẽ sử dụng Bridge ID để quyết định.

3. `Chọn Designated Port`: Trên mỗi segment của mạng (segment là một phần mạng nằm giữa hai switch hoặc giữa một switch và một thiết bị cuối), switch chọn một cổng làm Designated Port. Designated Port là cổng có đường đi ngắn nhất đến Root Bridge trên segment đó. Các cổng không được chọn là Designated Port sẽ ở trạng thái Blocking.

4. `Loại bỏ các đường đi dư thừa`: Sau khi chọn được Root Port và Designated Port cho mỗi switch, các đường đi dư thừa sẽ được loại bỏ bằng cách đặt các cổng không được chọn là Root Port hoặc Designated Port vào trạng thái Blocking. Điều này ngăn chặn việc xảy ra vòng lặp trong mạng.

5. `Kiểm tra và cập nhật topology`: STP liên tục kiểm tra các thay đổi trong mạng và thực hiện cập nhật topology nếu cần thiết. Nếu một đường đi chính thất bại (ví dụ: một cổng trên Root Bridge bị ngắt kết nối), STP sẽ chọn một đường đi thay thế và cập nhật các thông tin BPDU để thông báo cho các switch khác trong mạng.

## Thuộc tính ưu tiên (Priority)

1. Priority nhỏ nhất (chọn Bridge ID)

- Trong Spanning Tree Protocol (STP), thuộc tính `priority` (ưu tiên) được sử dụng để xác định switch nào sẽ trở thành `Root Bridge`. Switch với `priority thấp nhất` sẽ được chọn làm `Root Bridge`.

- Cụ thể, priority được sử dụng cùng với địa chỉ MAC của switch để tạo ra Bridge ID, một định danh duy nhất cho mỗi switch trong mạng. Bridge ID được sử dụng để so sánh và chọn Root Bridge.

- Mặc định, `priority` của mỗi switch là `32768`. Tuy nhiên, bạn có thể thay đổi giá trị này để ảnh hưởng đến quá trình chọn Root Bridge. Điều này thường được thực hiện bằng cách cấu hình priority trên các switch để đảm bảo rằng switch mong muốn trở thành Root Bridge có `priority thấp nhất`.

- Ví dụ, nếu bạn muốn switch A trở thành Root Bridge, bạn có thể thiết lập priority của switch A thành một giá trị thấp hơn so với các switch khác trong mạng. Khi đó, sau khi STP tính toán, switch A sẽ được chọn làm Root Bridge vì nó có Bridge ID thấp nhất.

2. Priority bằng nhau (so sánh MAC để chọn Bridge ID)

- Nếu hai hoặc nhiều switch có cùng priority, thì Bridge ID sẽ được quyết định bởi địa chỉ MAC của chúng. Switch với `địa chỉ MAC thấp hơn` sẽ được chọn làm `Root Bridge`.

- Trong trường hợp cả hai switch có cùng priority và cùng địa chỉ MAC (điều này rất không thường xuyên xảy ra vì địa chỉ MAC là duy nhất), thì STP sẽ sử dụng một thuật toán tie-breaker như là ID của port hoặc một thuộc tính khác để quyết định switch nào sẽ trở thành Root Bridge.

- Tuy nhiên, trong thực tế, việc hai switch có cùng priority và cùng địa chỉ MAC là rất hiếm, vì mỗi switch có một địa chỉ MAC riêng biệt và thường được cấu hình với một priority mặc định khác nhau để tránh sự xung đột khi chọn Root Bridge.

## Port Role

- Trong Spanning Tree Protocol (STP), vai trò của mỗi cổng trên switch được xác định bởi các trạng thái khác nhau, gọi là "port role". Các port role quan trọng trong STP bao gồm: 

1. `Root Port`: Đây là cổng trên switch mà có đường đi ngắn nhất tới Root Bridge. Mỗi switch chỉ có một Root Port. Root Port được chọn dựa trên độ dài của đường đi STP.

2. `Designated Port`: Trên mỗi segment của mạng (segment là một phần mạng nằm giữa hai switch hoặc giữa một switch và một thiết bị cuối), chỉ có một cổng được chọn làm Designated Port. Designated Port là cổng có đường đi ngắn nhất tới Root Bridge trên segment đó. Các gói tin gửi từ segment này sẽ được chuyển tới Root Bridge thông qua Designated Port của switch kết nối với segment đó.

3. `Blocking Port`: Các cổng không được chọn là Root Port hoặc Designated Port sẽ được đặt vào trạng thái Blocking. Các cổng ở trạng thái Blocking không tham gia vào việc chuyển tiếp dữ liệu, nhưng vẫn lắng nghe các gói tin BPDU (Bridge Protocol Data Unit) để phát hiện và ngăn chặn các vòng lặp.

4. `Forwarding Port`: Khi một cổng không phải là Root Port hoặc Designated Port, và không ở trong trạng thái Blocking, nó sẽ ở trong trạng thái Forwarding. Các gói tin dữ liệu sẽ được chuyển tiếp qua các cổng này.

## Cấu hình STP

1. Truy cập chế độ cấu hình (global configuration mode) trên switch

```sh
switch> enable
switch# configure terminal
```

2. Chọn loại STP mà bạn muốn cấu hình. Các phiên bản phổ biến của STP bao gồm:

- `STP (802.1D)`

```sh
spanning-tree mode pvst
```

- `Rapid STP (RSTP, 802.1w)`

```sh 
spanning-tree mode rapid-pvst
```

- `MSTP (Multiple Spanning Tree Protocol, 802.1s)`

```sh
spanning-tree mode mst
```

- Ví dụ, để cấu hình Rapid STP, bạn có thể nhập:

```sh
switch(config)# spanning-tree mode rapid-pvst
```
## Cấu hình Per VLAN STP

1. `Per VLAN Spanning Tree Protocol (PVSTP)` là một biến thể của Spanning Tree Protocol (STP) được Cisco phát triển để hỗ trợ STP trên mỗi VLAN trong mạng. 

2. Trong PVSTP, mỗi VLAN có một cây chuyển mạch riêng biệt, giúp tối ưu hóa các đường đi và cải thiện hiệu suất mạng trong các môi trường đa VLAN.

3. Cấu hình

- Truy cập chế độ cấu hình

```sh
switch> enable
switch# configure terminal
```

- Chọn chế độ PVSTP

```sh
switch(config)# spanning-tree mode pvst
```

- Thiết lập priority cho các VLAN

```sh
switch(config)# spanning-tree vlan <vlan-id> priority <priority-value>
```

## Kiểm tra cấu hình

1. Hiển thị thông tin về STP trên tất cả các VLAN

```sh
switch# show spanning-tree
```

2. Hiển thị thông tin chi tiết về STP trên một VLAN cụ thể

```sh
switch# show spanning-tree vlan <vlan-id>

```

3. Hiển thị thông tin về STP trên một cổng cụ thể

```sh
switch# show spanning-tree interface <interface-id>
```

4. Hiển thị thông tin về Root Bridge hiện tại

```sh
switch# show spanning-tree root
```