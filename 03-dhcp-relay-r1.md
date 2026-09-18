# 3. Configure R1 as a DHCP relay agent for 192.168.1.0/24

PC2 lives on R1's LAN (192.168.1.0/24), but the DHCP server is R2, which
is not directly connected to that subnet. R1 must relay DHCP broadcasts
from PC2 to R2 as unicast:

```
R1(config)# interface g0/1
R1(config-if)# ip helper-address 203.0.113.1
```

Notes:

- `ip helper-address` also forwards other UDP broadcast services (TFTP,
  DNS, NetBIOS, etc.) by default, not just DHCP — that's expected
  behavior, not a bug.
- No relay is needed on R2's own G0/1 (192.168.2.0/24), because R2 **is**
  the DHCP server and is directly connected to that subnet.
