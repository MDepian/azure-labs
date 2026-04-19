# 🔐 Azure Lab: Controlled RDP Access using ASG & NSG

## 📌 Overview
This lab demonstrates how to control RDP access in Azure using **Application Security Groups (ASG)** with a **Network Security Group (NSG)** at the subnet level.

---

## 🏗️ Architecture
- 1 Virtual Network (VNet)
- 1 Subnet
- 3 Virtual Machines:
  - VM1
  - VM2
  - VM3
- 1 Network Security Group (NSG) applied at **subnet level**

---

## 🎯 Objective
Allow RDP (Port 3389) access only to:
- VM1
- VM2  

Block access to:
- VM3

---

## ⚙️ Implementation Steps

1. Create an **Application Security Group (ASG)**
2. Add:
   - VM1
   - VM2  
   to the ASG
3. Leave VM3 outside the ASG
4. Configure an **NSG rule** at subnet level:
   - **Source:** Any (or your IP)
   - **Destination:** ASG
   - **Port:** 3389 (RDP)
   - **Protocol:** TCP
   - **Action:** Allow
   - **Priority:** Lower than default deny

---

## ✅ Results

| VM   | RDP Access |
|------|-----------|
| VM1  | ✅ Allowed |
| VM2  | ✅ Allowed |
| VM3  | ❌ Denied  |

---

## 💡 Key Takeaways
- ASG allows logical grouping of VMs without modifying NSG structure
- NSG at subnet level simplifies management
- Scalable and clean design for access control
- No need for multiple NSGs per VM

---

## 📚 Use Case
Ideal for:
- Securing administrative access
- Segmenting workloads within the same subnet
- Practicing real-world cloud security scenarios

---

## 🔗 More Information
Check the full lab implementation and steps in the repository.

---

## 🏷️ Tags
`Azure` `Networking` `NSG` `ASG` `RDP` `AZ-104` `Cloud Security`
