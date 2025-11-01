# Azure Secure Network Lab (PowerShell)
How to build a secure network in Azure using **PowerShell**

---

# Objective
- Deploy a secure Azure Virtual Network (VNet) using PowerShell.
- Configure a Network Security Group (NSG).
- Enforce inbound security rules.
- Demonstrate cloud automation, security best practices, and infrastructure‑as‑code (IaC) skills.

---

# Tools & Technologies
- Azure Portal
- PowerShell
- Azure Virtual Network
- Network Security Groups

# Steps Completed
1. Define the Variables (optional)
  - *$resourceGroup = "RG-SecureNet"*
  - *$location = "EastUS"*
  - *$vnetName = "VNet-Secure"*
  - *$subnetName = Subnet-FrontEnd"*
  - *$nsgName = "NSG-FrontEnd"*
2. Create Resource Group
  - **[New-AzResourceGroup -Name RG-SecureNet -Location EastUS]**
3. Create a Virtual Network
  - **[$vnet = New-AzVirtualNetwork -ResourceGroupName RG-SecureNet -Location EastUS -Name VNet-Secure -AddressPrefix "10.0.0.0/16"]**
4. Create a Subnet
  - **[Add-AzVirtualNetworkSubnetConfig -Name Subnet-FrontEnd -AddressPrefix "10.0.1.0/24" -VirtualNetwork $vnet]**
  - ***Commit the subnet to the Virtual Network***
    -  **[$vnet | Set-AzVirtualNetwork]**











