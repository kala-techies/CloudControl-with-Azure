#  Azure Networking: hub-Vnet with Public Subnets

This guide helps you quickly spin up a virtual network `hub-Vnet` with three **public subnets** using **Azure CLI**. Ideal for use directly from [Azure Cloud Shell](https://shell.azure.com/) or your local terminal (with CLI installed).

---

##  Prerequisites for Local Machine Setup

If you're using Azure CLI **locally** for the first time, follow these steps:

###  Step 1: Install Azure CLI

For **Windows**, **macOS**, or **Linux**, follow the official instructions:  
🔗 [Install Azure CLI](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli)

Or use one of the following commands:

#### Windows (PowerShell):
```powershell
Invoke-WebRequest -Uri https://aka.ms/installazurecliwindows -OutFile .\AzureCLI.msi; Start-Process msiexec.exe -Wait -ArgumentList '/I AzureCLI.msi /quiet'; rm .\AzureCLI.msi
````

#### macOS (Homebrew):

```bash
brew update && brew install azure-cli
```

#### Ubuntu/Debian:

```bash
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
```

---

###  Step 2: Sign in to Azure

```bash
az login
```

> This opens a browser to log in with your Azure credentials.

---

##  Spin Up Networking Resources via Azure Cloud Shell or Local

You can run the below commands **as-is** from **Azure Cloud Shell** or after installing `az` CLI locally.

---

##  Resource Group (Optional if already created)

```bash
az group create \
  --name myResourceGroup \
  --location eastus
```

---

##  Create Virtual Network and Subnets

```bash
az network vnet create \
  --resource-group myResourceGroup \
  --name hub-Vnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name managementSubnet \
  --subnet-prefix 10.0.1.0/24
```

```bash
az network vnet subnet create \
  --resource-group myResourceGroup \
  --vnet-name hub-Vnet \
  --name domainControllerSubnet01 \
  --address-prefix 10.0.2.0/24
```

```bash
az network vnet subnet create \
  --resource-group myResourceGroup \
  --vnet-name hub-Vnet \
  --name AzureFirewallSubnet \
  --address-prefix 10.0.3.0/24
```

>  Note: Azure Firewall **requires** the subnet to be named exactly `AzureFirewallSubnet`.

---

##  Verification

List your subnets:

```bash
az network vnet subnet list \
  --resource-group myResourceGroup \
  --vnet-name hub-Vnet \
  --output table
```

---

## 📌 Summary

| Component                | Name                       | Address Range |
| ------------------------ | -------------------------- | ------------- |
| Virtual Network          | `hub-Vnet`                 | `10.0.0.0/16` |
| Management Subnet        | `managementSubnet`         | `10.0.1.0/24` |
| Domain Controller Subnet | `domainControllerSubnet01` | `10.0.2.0/24` |
| Firewall Subnet          | `AzureFirewallSubnet`      | `10.0.3.0/24` |

