# Azure NSG Two-Gate Security Lab – RDP Access Case Study

## 📌 Overview
This lab demonstrates how Azure Network Security Groups (NSGs) control inbound traffic at two levels:
- Subnet Level
- Network Interface (NIC) Level

The main objective is to understand how RDP (Port 3389) access is evaluated when rules are applied at both layers.

---

## 🎯 Lab Objective
- Understand NSG rule processing
- Learn the difference between Subnet NSG and NIC NSG
- Test how Allow/Deny rules affect RDP connectivity
- Visualize the "two-gate" security concept in Azure networking

---

## 🏗️ Architecture
- Virtual Network (VNet)
- Subnet with NSG attached
- Virtual Machine (Windows)
- NIC with NSG attached
- RDP connection from Internet

---

## ⚙️ Configuration Steps

### 1. Create VNet
- Define Address Space (e.g., 10.0.0.0/16)

### 2. Create Subnet
- Define Subnet (e.g., 10.0.1.0/24)

### 3. Deploy Virtual Machine
- OS: Windows Server
- Enable Public IP for RDP access

### 4. Create NSGs
- NSG-Subnet → attach to Subnet
- NSG-NIC → attach to VM NIC

### 5. Configure RDP Rule
- Port: 3389
- Source: Any (for testing)
- Action: Allow or Deny based on experiment

---

## 🧪 Experiments

### Experiment A – Subnet DENY / NIC ALLOW
- Subnet NSG: Deny RDP
- NIC NSG: Allow RDP

**Result:** Connection Failed  
**Reason:** Traffic blocked at Subnet level

---

### Experiment B – Subnet ALLOW / NIC DENY
- Subnet NSG: Allow RDP
- NIC NSG: Deny RDP

**Result:** Connection Failed  
**Reason:** Traffic blocked at NIC level

---

### Experiment C – Subnet ALLOW / NIC ALLOW
- Subnet NSG: Allow RDP
- NIC NSG: Allow RDP

**Result:** Successful RDP Connection  
**Reason:** Traffic allowed through both layers

---

## 🔑 Key Takeaways
- NSG acts as a two-layer security mechanism
- Traffic must pass both Subnet and NIC rules
- Deny at any level overrides Allow
- Rule priority is critical in decision making

---

## 🚀 Conclusion
This lab provides a clear understanding of how Azure enforces layered network security using NSGs. It highlights the importance of proper rule design when securing cloud environments.

---

## 📎 Notes
- Use minimal open access in real environments (avoid "Any" source)
- Always follow least privilege principle
- Monitor NSG flow logs for deeper analysis

---

## 🏷️ Tags
Azure, NSG, Networking, Cloud Security, AZ-104, Hands-On Lab
