# Bình bầu DR & BDR trong OSPF

- Để cấu hình ưu tiên (priority) trên các giao diện để xác định Router có ưu tiên để trở thành Designated Router (DR) hoặc Backup Designated Router (BDR) trong mạng OSPF, sử dụng lệnh `ip ospf priority` trong chế độ cấu hình giao diện.

- Cấu hình cụ thể:

```sh
Router(config)# interface interface_type interface_number    // Đi vào chế độ cấu hình cho giao diện cụ thể
Router(config-if)# ip ospf priority priority_value           // Cấu hình ưu tiên OSPF cho giao diện, priority_value có giá trị từ 0 đến 255
```

> Trong đó:

+ `interface_type`: Loại giao diện, ví dụ: Ethernet, GigabitEthernet, Loopback, v.v.

+ `interface_number`: Số giao diện, ví dụ: 0/0, 0/1, 1, v.v.

+ `priority_value`: Giá trị ưu tiên của Router trong mạng OSPF. Router có `priority_value cao nhất` sẽ được chọn làm `DR` 
và Router có `priority_value cao nhì` sẽ được chọn làm `BDR`. Một Router có `priority_value là 0` sẽ không được chọn làm `DR` hoặc `BDR`.

- Ví dụ:

```sh
Router(config)# interface Ethernet0/0
Router(config-if)# ip ospf priority 255   // Đặt priority là 255 cho Router 192.168.1.1
```

```sh
Router(config)# interface Ethernet0/0
Router(config-if)# ip ospf priority 254   // Đặt priority là 254 cho Router 192.168.1.2
```
> Trong trường hợp này, Router có địa chỉ IP là `192.168.1.1` sẽ được ưu tiên hơn để trở thành `DR`, trong khi Router có địa chỉ IP là `192.168.1.2` sẽ được ưu tiên hơn để trở thành `BDR`.

- Sau khi cấu hình xong priority có thể kiểm tra bằng lệnh. 
	`Router# show ip ospf interface f0/0` 

