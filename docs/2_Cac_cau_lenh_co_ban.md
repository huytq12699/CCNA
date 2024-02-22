# Các chế độ cấu hình

- `Router>`(chế độ user mode)

- `Router>enable` (vào chế độ Privileged EXEC Mode) 

- `Router#configure terminal` (vào chế độ Configuration Mode) 

# Cấu hình đặt tên và password cho router

- `Router(config)#hostname <tên_muốn_đặt>` (đặt tên cho router) 

- `Router(config)#enable password <pass_muốn đặt>` (cấu hình pass ko mã hóa) 

- `Router(config)#enable secret <pass_muốn_đặt>` (cấu hình pass được mã hóa bằng MD5)

# Cấu hình các đường truy cập (console, aux và vty) 

- Cấu hình cổng console

```sh
Router(config)#line console 0 
Router(config-line)#password <pass_cho_cổng_console> (có thể khác pass của router) 
Router(config-line)#login (bắt buộc phải có để chế độ đặt pass cho cổng console có hiệu lực)
```

- Cấu hình cổng aux

```sh
Router(config)#line aux 0 
Router(config-line)#password <pass_cho_cổng_aux> (có thể khác pass của router) 
Router(config-line)#login (bắt buộc phải có để chế độ đặt pass cho cổng console có hiệu lực) 
```

- Cấu hình cổng vty (cổng telnet)

```sh
Router(config)#line vty 0 4 (chỉ cấu hình 5 đường telnet trong 1 thời điểm). 
Router(config-line)#password <pass_cho_cổng_vty> (có thể khác pass của router) 
Router(config-line)#login (bắt buộc phải có để chế độ đặt pass cho cổng vty có hiệu lực) 
```
- Câu lệnh để mã hóa tất cả mật khẩu

`Router(config)#service password-encryption `

# Cấu hình địa chỉ ip cho interface

```sh
Router(config)#interface tên_cổng (vào interface) 
Router(config-if)#no shutdown (cho phép interface hoạt động) 
Router(config-if)#clock rate 64000 (đặt thời gian đồng bộ giữa 2 router, chỉ dùng với đường serial) 
Router(config-if)#ip address địa_chỉ_ip subnet_mask (đặt địa chỉ ip cho interface)
```