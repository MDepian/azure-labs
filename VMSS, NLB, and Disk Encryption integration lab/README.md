# Azure Secure Infrastructure Lab: VMSS, NLB, and Disk Encryption

## 🚀 Project Overview
This lab demonstrates a production-grade hardened infrastructure in Azure. The goal was to eliminate direct public access to Virtual Machines and implement "Encryption at Rest" using Customer-Managed Keys (CMK).

## 🏗 Architecture
The environment consists of a private backend pool where VMs have no Public IPs. Access is managed through a central entry point, and data is secured via the Azure Disk Encryption (ADE) extension linked to a Key Vault.

### Key Features:
- **Zero Public IPs:** All compute nodes are private to reduce the attack surface.
- **NAT-Based Management:** RDP access is handled via **Inbound NAT Rules** on a Standard Load Balancer.
- **Disk Encryption Set (DES):** Acts as the bridge between **Azure Key Vault** and VM disks.
- **Identity-Based Security:** Uses a **System-Assigned Managed Identity** for the DES to access the encryption keys.

---

## 🛠 Components Configured

### 1. Networking & Load Balancing
- **Azure Standard Load Balancer:** Configured with a Frontend Public IP.
- **Inbound NAT Rules:** - Port `50001` -> VM1 (Port 3389)
    - Port `50002` -> VM2 (Port 3389)
- **NSG Rules:** Hardened to allow inbound traffic only on the specified NAT ports.

### 2. Security & Encryption
- **Key Vault:** Stores the RSA 2048-bit encryption key.
- **Disk Encryption Set:** Created to manage the relationship between the key and the disks.
- **RBAC:** Granted `Key Vault Crypto Service Encryption User` to the DES Managed Identity.
- **Encryption Type:** `EncryptionAtRestWithCustomerKey`.

---

## 💻 Configuration (Lab Steps)

### Phase 1: Secure Access
1. Create a **Virtual Network (VNet)** and a Backend Subnet.
2. Deploy a **Standard Load Balancer**.
3. Create **Inbound NAT Rules** for RDP management.
4. Deploy VMs/VMSS into the subnet with **Public IP set to "None"**.

### Phase 2: Disk Encryption
1. Deploy an **Azure Key Vault** (Premium or Standard).
2. Create an **RSA Key** inside the vault.
3. Deploy a **Disk Encryption Set (DES)** and link it to the key.
4. Go to **Identity** on the DES and enable "System Assigned".
5. In Key Vault **Access Control (IAM)**, assign the DES identity the permission to wrap/unwrap keys.
6. Update the VM/VMSS disks to use the **Disk Encryption Set**.

---

## 🔍 Verification Commands

### Check Public IP Status (CLI)
```bash
az vm list-ip-addresses --resource-group YourRG --name YourVM
