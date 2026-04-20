# Azure VNet-to-VNet VPN Gateway Lab

## 📌 Project Overview
This project demonstrates the implementation of a secure, encrypted interconnect between two isolated Azure Virtual Networks (VNets) using **Virtual Network Gateways**. This architecture simulates a cross-region or cross-subscription connection, ensuring private communication between resources in different IP address spaces.

## 🏗️ Architecture
The lab consists of two distinct environments (Alpha and Beta) connected via a Route-Based VPN tunnel.



### Networking Specifications
| Resource | VNet-Alpha (Hub-A) | VNet-Beta (Hub-B) |
| :--- | :--- | :--- |
| **Resource Group** | `RG-Alpha` | `RG-Beta` |
| **Address Space** | `10.0.0.0/16` | `192.168.0.0/16` |
| **Workload Subnet** | `10.0.1.0/24` | `192.168.1.0/24` |
| **Gateway Subnet** | `10.0.255.0/27` | `192.168.255.0/27` |

## 🚀 Key Features & Tasks
- **Parallel Gateway Deployment:** Provisioned two `VpnGw1` (Generation 1) Route-Based Gateways.
- **Secure Authentication:** Implemented a Site-to-Site (S2S) connection using a **Pre-Shared Key (PSK)**.
- **Security Hardening:** - Configured **Network Security Groups (NSGs)** to allow ICMP and RDP traffic.
  - Managed **Guest OS Firewalls** (Windows) to enable ICMP echo requests via PowerShell.
- **Connectivity Validation:** Verified end-to-end routing by performing cross-VNet pings between virtual machines.

## 🛠️ Deployment Steps
1. **Infrastructure Setup:** Created Resource Groups, VNets, and the mandatory `GatewaySubnet`.
2. **Gateway Provisioning:** Deployed Virtual Network Gateways (Approx. 45-minute deployment time).
3. **Connection Bridging:** Created bidirectional `VNet-to-VNet` connection objects using identical PSKs.
4. **Validation:** Logged into `VM-Alpha` and successfully pinged `192.168.1.4`.

## 📝 Lessons Learned
- **DNS/Routing Logic:** Understanding how Azure automatically handles routing between the `10.x` and `192.168.x` spaces once the tunnel is "Connected."
- **Latency Considerations:** Noticed the difference in setup complexity and performance compared to standard VNet Peering.
- **Troubleshooting:** Identified that internal OS firewalls often block pings even when the network tunnel is healthy.

## 🔧 Tools Used
- Azure Portal
- PowerShell (Firewall & Connectivity Testing)
- Markdown (Documentation)
