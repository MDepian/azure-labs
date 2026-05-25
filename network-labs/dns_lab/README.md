# Azure Private DNS Zone Architecture Lab

This repository contains a hands-on lab designed to demonstrate the implementation, auto-registration mechanics, and troubleshooting of an **Azure Private DNS Zone** within a single Virtual Network (VNet). 

By completing this lab, you will understand the separation between the **Control Plane** (DNS registration/linking) and the **Data Plane** (network traffic and OS-level firewalls).

---

## 🛠️ Lab Component Blueprint

| Component | Resource Name | Configuration Details |
| :--- | :--- | :--- |
| **Virtual Network** | `Lab-VNet` | Address Space: `10.0.0.0/16` |
| **Subnet** | `vmsubnet` | Address Range: `10.0.0.0/24` |
| **Private DNS Zone** | `mystatichome.local` | Private namespace hidden from the public internet |
| **VNet Link** | `lab-vnet-link` | Linked to `Lab-VNet` with **Autoregistration Enabled** |
| **Virtual Machine A** | `VM-A` | Initiator Machine (IP: `10.0.0.4`) |
| **Virtual Machine B** | `VM-B` | Target Machine (IP: `10.0.0.5`) |
| **Network Security Group**| Default NSG | Built-in rule `AllowVnetInbound` permits internal VNet traffic |

---

## 🚀 Step-by-Step Deployment Guide

### Phase 1: Infrastructure Deployment (Control Plane)
1. **Create the Core Network:** Deploy `Lab-VNet` with the address space `10.0.0.0/16` and add a subnet named `vmsubnet` (`10.0.0.0/24`).
2. **Deploy the Private DNS Zone:** Create a Private DNS zone named `mystatichome.local`. 
3. **Link & Enable Autoregistration:** Navigate to your Private DNS Zone -> **Virtual Network Links** -> **Add**. Select `Lab-VNet` and crucially check the **"Enable auto registration"** box.
4. **Deploy the Test VMs:** Provision `VM-A` and `VM-B` inside `vmsubnet`. 
5. **Verify DNS Sync:** Wait 2 minutes after VM deployment. Refresh your Private DNS Zone page to confirm that Dynamic `A Records` have automatically appeared for both VMs pointing to their respective `10.0.0.x` internal IPs.

### Phase 2: Host Firewall Configuration (Data Plane)
By default, Azure's default NSG allows internal traffic via the `AllowVnetInbound` rule. However, Windows Server OS internal firewalls block ICMP (Ping) requests. 

To allow connectivity testing, log into **both VMs** and execute the following administrative command to bypass or configure the firewall:

* **Option A: Allow ICMP Traffic securely (Recommended)**
    ```powershell
    New-NetFirewallRule -DisplayName "Allow ICMPv4-In" -Protocol ICMPv4 -IcmpType 8 -Enabled True -Action Allow
    ```
* **Option B: Completely drop the OS Firewall for quick lab testing**
    ```powershell
    Set-NetFirewallProfile -Profile Domain,Public,Private -Enabled False
    ```

---

## 🧪 Validation & Testing

Log into **VM-A** via RDP/SSH and open PowerShell/Terminal to execute the data flow sequence shown in the diagram:

### 1. Test DNS Name Resolution
Query the Azure Recursive Resolver (`168.63.129.16`) to ensure the name translates into an internal IP address:
```powershell
Resolve-DnsName vm-b.mystatichome.local
