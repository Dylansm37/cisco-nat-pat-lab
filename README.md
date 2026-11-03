# NAT and PAT Configuration Lab

## Overview

This lab demonstrates Network Address Translation (NAT) and Port Address Translation (PAT) using Cisco routers in Packet Tracer.

The lab focuses on translating private inside IP addresses into an outside-facing IP address, allowing internal devices to communicate with an external network. PAT overload allows multiple inside devices to share a single outside IP address using unique identifiers for their connections.

## Objectives

- Configure router interfaces and IP addressing.
- Configure a standard ACL to identify inside network traffic.
- Configure PAT using an outside interface address.
- Identify and configure NAT inside and outside interfaces.
- Verify NAT translations using Cisco IOS commands.
- Troubleshoot incorrect PAT interface references.
- Understand inside local, inside global, outside local, and outside global addresses.

## IP Addressing

| **Device** | **Interface** | **IP Address** |
|---|---|---|
| PC1 | NIC | 192.168.1.10/24 |
| R1 | G0/0 | 192.168.1.1/24 |
| R1 | G0/1 | 203.0.113.1/30 |
| ISP Router | G0/0 | 203.0.113.2/30 |
| ISP Router | G0/1 | 198.51.100.1/24 |
| Server | NIC | 198.51.100.10/24 |

## Technologies

- Cisco IOS
- Network Address Translation (NAT)
- Port Address Translation (PAT)
- Standard Access Control Lists (ACLs)
- Cisco Packet Tracer

## NAT Configuration

Configured standard ACL 10 to identify traffic originating from the inside network:

```cisco
access-list 10 permit 192.168.1.0 0.0.0.255
```

Configured PAT using the IP address assigned to R1's outside interface:

```cisco
ip nat inside source list 10 interface GigabitEthernet0/1 overload
```

Configured NAT interface roles:

```cisco
interface GigabitEthernet0/0
 ip nat inside

interface GigabitEthernet0/1
 ip nat outside
```

## Verification

Commands used:

```cisco
show ip interface brief
show access-lists
show ip nat translations
show ip nat statistics
show running-config
```

Successful PAT translation example:

| **Translation Type** | **IP Address** |
|---|---|
| Inside Local | 192.168.1.10 |
| Inside Global | 203.0.113.1 |
| Outside Local | 198.51.100.10 |
| Outside Global | 198.51.100.10 |

## Files

- `lab.pkt`: Packet Tracer topology
- `configs/`: Router configuration files
- `topology.png`: Network topology
- `troubleshooting.md`: Troubleshooting notes
