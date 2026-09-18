# DHCP Server + Relay Agent Lab

## Topology

```
   192.168.2.0/24                 203.0.113.0/30                192.168.1.0/24
  [SW1]---G0/1 (.1)[R2]G0/0(.1)---------------G0/0(DHCP)[R1]G0/1(.1)---[SW2]
    |                                                                    |
  [PC1]                                                                [PC2]
```

| Device | Interface | Network            | IP Address        | Role                     |
|--------|-----------|---------------------|--------------------|--------------------------|
| R2     | G0/1      | 192.168.2.0/24      | 192.168.2.1        | Gateway for PC1's subnet |
| R2     | G0/0      | 203.0.113.0/30      | 203.0.113.1        | WAN, static, DHCP server |
| R1     | G0/1      | 192.168.1.0/24      | 192.168.1.1        | Gateway for PC2's subnet |
| R1     | G0/0      | 203.0.113.0/30      | DHCP client (`.2`) | WAN, learns from R2      |

**R2 is the DHCP server** for all three pools. **R1's LAN (192.168.1.0/24) is not
directly connected to R2**, so R1 must relay DHCP broadcasts from PC2 to R2 — that's
the point of question 3.

## Files

| File | Question |
|------|----------|
| `01-dhcp-pools-r2.md`      | Configure the DHCP pools on R2 |
| `02-dhcp-client-r1.md`     | Configure R1's G0/0 as a DHCP client |
| `03-dhcp-relay-r1.md`      | Configure R1 as a DHCP relay agent |
| `04-pc-dhcp-requests.md`   | Request IPs from PC1 and PC2 CLI |
