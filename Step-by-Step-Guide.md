# 🚀 Advanced Azure Storage Lab — Professional Step-by-Step Guide

## 🎯 Scenario
**Contoso Corporation** requires a secure Azure storage environment for:
- shared company files
- backups
- application data

The solution must support:
- private connectivity
- secure file access
- RBAC permissions
- lifecycle management
- DNS integration

---

# 🏗️ Architecture

![Architecture](./diagrams/architecture.png)

---

# 🛠️ STEP 1 — Create Resource Group

Go to:
## Resource Groups → Create

### Settings

| Field | Value |
|---|---|
| Name | `rg-storage-advanced` |
| Region | `UAE North` |

Click:
- Review + create
- Create

---

# 🌐 STEP 2 — Create Virtual Network & Subnet

Go to:
## Virtual Networks → Create

### VNet Settings

| Field | Value |
|---|---|
| Name | `vnet-storage` |
| Address Space | `10.5.0.0/16` |

### Subnet Settings

| Field | Value |
|---|---|
| Name | `subnet-storage` |
| Address Range | `10.5.1.0/24` |

Click:
- Review + create
- Create

---

# 💻 STEP 3 — Create Management VM

Go to:
## Virtual Machines → Create

### Settings

| Field | Value |
|---|---|
| Name | `vm-storage-admin` |
| Image | `Windows Server 2022` |
| VNet | `vnet-storage` |
| Subnet | `subnet-storage` |

Create the VM.

---

# 🗂️ STEP 4 — Create Storage Account

Go to:
## Storage Accounts → Create

### Settings

| Field | Value |
|---|---|
| Name | `rubastorageprod` |
| Performance | `Standard` |
| Redundancy | `LRS` |
| Kind | `StorageV2` |
| Region | `UAE North` |

### Networking
- Public access: Enabled (temporary)

Click:
- Review + create
- Create

---

# 📦 STEP 5 — Create Blob Containers

Inside the Storage Account:

Go to:
## Data Storage → Containers

Create:
- `backups`
- `documents`
- `logs`

---

# 🧰 STEP 6 — Install & Connect Azure Storage Explorer

Inside:
## vm-storage-admin

Install:
## Azure Storage Explorer

Sign in using your Azure account.

---

# 🔐 STEP 7 — Configure RBAC

Go to:
## Storage Account → Access Control (IAM)

Click:
## + Add Role Assignment

Assign:
## Storage Blob Data Contributor

To:
- your user account

---

# 🔑 STEP 8 — Generate SAS Token

Go to:
## Storage Account → Shared Access Signature

### Permissions
Enable:
- Read
- Write
- List

Generate the SAS token and URL.

---

# 📁 STEP 9 — Create Azure File Share

Go to:
## File Shares → + File Share

### Settings

| Field | Value |
|---|---|
| Name | `company-share` |

Create the file share.

---

# 🔗 STEP 10 — Mount File Share to VM

Inside the File Share:

Click:
## Connect

Copy the provided PowerShell script and run it inside:
## vm-storage-admin

This mounts the Azure File Share to the VM.

---

# 🔒 STEP 11 — Create Private Endpoints

Go to:
## Private Endpoints → Create

Create two private endpoints:

| Endpoint | Target |
|---|---|
| `pe-blob` | Blob |
| `pe-file` | File |

### Network Settings

| Field | Value |
|---|---|
| VNet | `vnet-storage` |
| Subnet | `subnet-storage` |

---

# 🌐 STEP 12 — Create Private DNS Zones

Go to:
## Private DNS Zones → Create

Create:

| DNS Zone |
|---|
| `privatelink.blob.core.windows.net` |
| `privatelink.file.core.windows.net` |

---

# 🔗 STEP 13 — Link DNS Zones to VNet

Inside each Private DNS Zone:

Go to:
## Virtual Network Links → + Add

Select:
- `vnet-storage`

---

# 🚫 STEP 14 — Disable Public Access

Open:
## Storage Account → Networking

Set:
## Public network access = Disabled

Save changes.

---

# 🧪 STEP 15 — Test Private Connectivity

Inside:
## vm-storage-admin

Run:

```powershell
nslookup rubastorageprod.blob.core.windows.net
nslookup rubastorageprod.file.core.windows.net
```

---

# ✅ Expected Result

The DNS resolution should return:
- Private IP addresses
- Not public IPs

This confirms that Private Link is working correctly.

---

# ♻️ STEP 16 — Configure Lifecycle Management

Go to:
## Storage Account → Data Management → Lifecycle Management

Click:
## + Add a rule

### Rule Settings

| Field | Value |
|---|---|
| Rule Name | `old-backups-to-cool` |
| Condition | Last modified > 30 days |
| Action | Move to Cool tier |

Save the rule.

---

# 💡 Benefits

- Reduced storage costs
- Automated storage optimization
- Secure private connectivity
- Improved storage governance

---

# 📸 Recommended Screenshots

Take screenshots of:

1. VNet & Subnet  
2. Storage Account  
3. Blob Containers  
4. RBAC Assignment  
5. SAS Token page  
6. Azure File Share  
7. Private Endpoint  
8. Private DNS Zones  
9. nslookup result  
10. Lifecycle Management Rule

---

# 💡 Skills Demonstrated

- Azure Storage
- Azure File Shares
- RBAC
- SAS Tokens
- Private Link
- Private DNS
- Lifecycle Management
- Azure Networking
- Secure Cloud Architecture
