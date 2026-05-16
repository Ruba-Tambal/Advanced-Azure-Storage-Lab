# Step-by-Step Guide - Advanced Azure Storage Lab

## 🎯 Scenario
**Contoso Corporation** needs a secure storage environment for shared files, backups, and application data with private access.

## 🏗️ Architecture

![Architecture](./diagrams/architecture.png)

### STEP 1 — Create Resource Group
- Name: `rg-storage-advanced`
- Region: **UAE North**

### STEP 2 — Create Virtual Network & Subnet
- VNet Name: `vnet-storage` (`10.5.0.0/16`)
- Subnet Name: `subnet-storage` (`10.5.1.0/24`)

### STEP 3 — Create Management VM
- Name: `vm-storage-admin`
- Windows Server 2022
- Subnet: `subnet-storage`

### STEP 4 — Create Storage Account
- Name: `rubastorageprod`
- Kind: StorageV2
- Region: UAE North
- Public access: Enabled (temporary)

### STEP 5 — Create Blob Containers
- `backups`, `documents`, `logs`

### STEP 6 — Install & Connect Azure Storage Explorer
- Install on `vm-storage-admin`
- Sign in with Azure Account

### STEP 7 — Configure RBAC
- Assign **Storage Blob Data Contributor** to your user

### STEP 8 — Generate SAS Token
- Generate SAS with Read/Write/List permissions

### STEP 9 — Create Azure File Share
- Name: `company-share`
- Mount it to the VM using the provided PowerShell script

### STEP 10 — Create Private Endpoints
- One for `blob`
- One for `file`

### STEP 11 — Create Private DNS Zones
- `privatelink.blob.core.windows.net`
- `privatelink.file.core.windows.net`
- Link both to `vnet-storage`

### STEP 12 — Disable Public Access
- Set Public network access = **Disabled**

### STEP 13 — Test Private Connectivity
```powershell
nslookup rubastorageprod.blob.core.windows.net
nslookup rubastorageprod.file.core.windows.net
