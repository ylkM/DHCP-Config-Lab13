# 2. Configure R1's G0/0 as a DHCP client

```
R1(config)# interface g0/0
R1(config-if)# ip address dhcp
R1(config-if)# no shutdown
```

## What IP address did it configure?

`203.0.113.0/30` has only two usable host addresses: `.1` and `.2`
(`.0` is the network address, `.3` is the broadcast address). `.1` is
excluded/reserved for R2 itself (POOL3), so:

> **R1's G0/0 is assigned `203.0.113.2 / 255.255.255.252`**, with default
> gateway `203.0.113.1` (R2).

Verify with:
```
R1# show ip interface brief
R1# show dhcp lease
```
