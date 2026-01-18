# Network-Design-CCNA
Enterprise network design with VLANs, HSRP, secure SSH access, PAT, and centralized monitoring using Cisco Packet Tracer.
# Enterprise Network Lab

This project demonstrates the design and implementation of a small enterprise network using Cisco Packet Tracer.

## Topology Overview
The network consists of multiple VLANs, redundant routers, and centralized monitoring services.

![Topology](images/topology.jpeg)

## Implemented Features
- Inter-VLAN Routing using router sub-interfaces
- VLAN segmentation (HR, IT, Sales)
- HSRP for default gateway redundancy (Primary & Backup routers)
- Secure SSH access restricted to Admin only using ACL
- PAT (NAT Overload) for outbound connectivity
- Centralized monitoring with Syslog, NetFlow, and NTP
- Static IP addressing for all end devices

## VLANs
| VLAN | Name  | Subnet |
|-----|------|--------|
| 10  | HR   | 192.168.10.0/26 |
| 20  | IT   | 192.168.10.64/26 |
| 30  | Sales| 192.168.10.128/26 |
| 99  | Managmiant| 192.168.10.192/26 |

## Security
- SSH enabled on routers
- Access to VTY lines restricted to Admin IP only
- Network segmentation using VLANs

## NAT Configuration (PAT)
```bash
access-list 10 permit 192.168.10.0 0.0.0.63
ip nat inside source list 10 interface g0/0/1 overload
username admin privilege 15 secret admin123

ip access-list standard ADMIN_ONLY
 permit host 192.168.10.200

line vty 0 4
 login local
 transport input ssh
 access-class ADMIN_ONLY in



Monitoring & Management

Syslog server for centralized logging
NetFlow enabled on router interfaces
NTP used for time synchronization
