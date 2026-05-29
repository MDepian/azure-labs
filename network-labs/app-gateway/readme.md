# Azure Application Gateway Path-Based Routing Lab

## Overview
This project demonstrates a secure Azure networking architecture using Azure Application Gateway v2 with Path-Based Routing.

The Application Gateway routes traffic to different backend virtual machines based on URL paths.

---

## Architecture

- Azure Virtual Network (VNet)
- Azure Application Gateway v2
- Network Security Groups (NSGs)
- Two IIS Virtual Machines
- Path-Based Routing Rules

### Routing Rules
| Path | Backend |
|------|----------|
| `/` | VM1 |
| `/video/*` | VM2 |

---

## Security
- Separate subnets for Application Gateway and backend servers
- NSGs for traffic filtering
- Backend VMs use private IP addresses only
- Controlled inbound access through Application Gateway

---

## Result
- Centralized traffic management
- Secure backend isolation
- Successful path-based routing implementation
- Improved scalability and organization

---

## Technologies Used
- Microsoft Azure
- Azure Application Gateway
- Azure Networking
- IIS Web Server
- NSGs

---

## Architecture Diagram

![Architecture Diagram](./diagram.png)

---

## GitHub Repository
[ Add Your Repo Link Here ]

---

## Cloud Mechanics Community
[ Add Telegram Link Here ]

---

## Author
Mahmoud Debo

#Azure #CloudComputing #AzureNetworking #CloudSecurity
