# 1. Configure DHCP pools on R2

R2 is the DHCP server for the whole topology (POOL1, POOL2, POOL3).

```
R2(config)# ip dhcp excluded-address 192.168.1.1 192.168.1.10
R2(config)# ip dhcp excluded-address 192.168.2.1 192.168.2.10
R2(config)# ip dhcp excluded-address 203.0.113.1 203.0.113.1

R2(config)# ip dhcp pool POOL1
R2(dhcp-config)# network 192.168.1.0 255.255.255.0
R2(dhcp-config)# default-router 192.168.1.1
R2(dhcp-config)# dns-server 8.8.8.8
R2(dhcp-config)# domain-name jeremysitlab.com
R2(dhcp-config)# exit

R2(config)# ip dhcp pool POOL2
R2(dhcp-config)# network 192.168.2.0 255.255.255.0
R2(dhcp-config)# default-router 192.168.2.1
R2(dhcp-config)# dns-server 8.8.8.8
R2(dhcp-config)# domain-name jeremysitlab.com
R2(dhcp-config)# exit

R2(config)# ip dhcp pool POOL3
R2(dhcp-config)# network 203.0.113.0 255.255.255.252
R2(dhcp-config)# exit
```

> `excluded-address` must be configured globally, outside the pool. It's easy to
> forget, and is the #1 reason a pool hands out `.1` by mistake.

POOL1's default gateway (`192.168.1.1`) is R1, and POOL2's default gateway
(`192.168.2.1`) is R2 itself — both routers' LAN-facing interfaces.
