# Centralized DHCP Server with DHCP Relay

## 1. Project Overview

This project demonstrates centralized DHCP address allocation using a dedicated server in Cisco Packet Tracer.

A Cisco 2911 router performs inter-VLAN routing and DHCP relay, while a dedicated Server-PT device provides IP addresses to clients across multiple VLANs.

## 2. Network Devices

| Device | Model | Purpose |
|---|---|---|
| Router | Cisco 2911 | Inter-VLAN routing and DHCP relay |
| Switch | Cisco 2960 | VLAN management and switching |
| Server | Server-PT | Centralized DHCP server |
| PCs | PC-PT | DHCP clients |

## 3. VLAN and IP Addressing Plan

| Department | VLAN | Network | Default Gateway |
|---|---:|---|---|
| ADMIN | 10 | 192.168.10.0/24 | 192.168.10.1 |
| HR | 20 | 192.168.20.0/24 | 192.168.20.1 |
| IT | 30 | 192.168.30.0/24 | 192.168.30.1 |
| FINANCE | 40 | 192.168.40.0/24 | 192.168.40.1 |
| SERVER | 99 | 192.168.99.0/24 | 192.168.99.1 |

### DHCP Server Static Configuration

- IP Address: 192.168.99.10
- Subnet Mask: 255.255.255.0
- Default Gateway: 192.168.99.1
- DNS Server: 8.8.8.8

## 4. DHCP Server Configuration

A dedicated Server-PT device was configured as the DHCP server.

Four DHCP pools were created:

| Pool | Gateway | Starting IP |
|---|---|---|
| ADMIN | 192.168.10.1 | 192.168.10.11 |
| HR | 192.168.20.1 | 192.168.20.11 |
| IT | 192.168.30.1 | 192.168.30.11 |
| FINANCE | 192.168.40.1 | 192.168.40.11 |

Common settings:
- Subnet Mask: 255.255.255.0
- DNS Server: 8.8.8.8
- Maximum Users: 200 per pool

## 5. DHCP Relay Configuration

The router was configured with the `ip helper-address` command on each client VLAN subinterface.

```cisco
interface GigabitEthernet0/0.10
 ip helper-address 192.168.99.10

interface GigabitEthernet0/0.20
 ip helper-address 192.168.99.10

interface GigabitEthernet0/0.30
 ip helper-address 192.168.99.10

interface GigabitEthernet0/0.4
 ip helper-address 192.168.99.10
```

The helper address forwards DHCP client broadcasts to the centralized DHCP server.

## 6. Verification Commands

The following Cisco IOS commands were used:

| Command | Purpose |
|---|---|
| `show vlan brief` | Verify VLAN configuration |
| `show interfaces trunk` | Verify trunk links |
| `show ip interface brief` | Check router interfaces |
| `show ip interface GigabitEthernet0/0.10` | Verify DHCP relay address |
| `show running-config` | Review router configuration |

## 7. Testing and Results

The following tests were performed:

- Verified connectivity between the DHCP server and its default gateway.
- Verified that all router VLAN subinterfaces were up/up.
- Verified DHCP relay configuration on all four client VLANs.
- Configured four DHCP scopes on the dedicated server.
- Successfully obtained DHCP addresses on all four PCs.

## 8. Key Learning Outcomes

- Understanding centralized DHCP architecture.
- Configuring a dedicated DHCP server.
- Creating DHCP scopes for multiple subnets.
- Understanding DHCP relay agents.
- Configuring `ip helper-address`.
- Understanding why DHCP broadcasts do not normally cross router interfaces.
- Verifying network connectivity and DHCP operation.

## 9. Conclusion

This lab demonstrates how a centralized DHCP server can provide dynamic IP address allocation to clients in multiple VLANs through a router configured as a DHCP relay agent.

**Project:** Small Office Centralized DHCP Lab  
**Version:** 1.0  
**Platform:** Cisco Packet Tracer