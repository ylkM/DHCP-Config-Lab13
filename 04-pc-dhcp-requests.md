# 4. Use the CLI of PC1 and PC2 to request an IP from DHCP

On Packet Tracer end devices, use the PC's command-line "ip" utility:

```
PC1> ipconfig /release
PC1> ipconfig /renew
```

```
PC2> ipconfig /release
PC2> ipconfig /renew
```

## Expected results

| PC  | Pool used | Address received                    | Gateway     | Path                           |
|-----|-----------|--------------------------------------|-------------|---------------------------------|
| PC1 | POOL2     | 192.168.2.11 (first free after .10)  | 192.168.2.1 | Direct broadcast to R2         |
| PC2 | POOL1     | 192.168.1.11 (first free after .10)  | 192.168.1.1 | Relayed by R1 → unicast to R2  |

Confirm with `ipconfig /all` on each PC, and on R2 with:
```
R2# show ip dhcp binding
```
You should see bindings for both the 192.168.1.0/24 and 192.168.2.0/24
pools, proving the relay from R1 is working.

## Troubleshooting

- If PC2 doesn't get an address, double-check `ip helper-address` is on
  R1's **G0/1** (the LAN-facing interface), not G0/0.
- If R1's G0/0 doesn't pick up an address, confirm `no shutdown` was
  issued and that R2's G0/0 is up with
  `ip address 203.0.113.1 255.255.255.252` configured statically (not
  via DHCP — R2 is the server, so this interface must be static).
