# Định tuyến tĩnh

Có 2 cách cấu hình Static Route

- Cách 1: cấu hình theo "next hop" address

```sh
 Router(config)#ip route địa_chỉ_mạng_muốn_quảng_bá subnet_mask 
địa_chỉ_ip_của_interface_nối_với_mạng_muốn_quảng_bá
```
- Cách 2: Cấu hình theo exit interface

```sh
Router(config)#ip route địa_chỉ_mạng_muốn_quảng_bá subnet_mask 
interface_nối_với_mạng_muốn_quảng_bá
```
## Cấu hình Default Route

```sh
Router(config)#ip route 0.0.0.0 0.0.0.0 [exit interface/ip address]
```


