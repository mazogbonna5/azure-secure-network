# Building a Secure Virtual Network with Azure PowerShell
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

---

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

5. Create a Network Security Group (NSG)
  - **[$nsg = New-AzNetworkSecurityGroup -ResourceGroupName RG-SecureNet -Location EastUS -Name NSG-FrontEnd]**

6. Add Secure Rules *(Allow HTTPS Only)*
  - **[Add-AzNetworkSecurityRuleConfig -Name "Allow-HTTPS" -NetworkSecurityGroup $nsg -Protocol "Tcp" -Direction "Inbound" -Priority 100 -SourceAddressPrefix " * " -SourcePortRange " * " -DestinationAddressPrefix " * " -DestinationPortRange 443 -Access "Allow"]**
    
  - ***Update the Network Security Group (NSG)***
    - **[$nsg | Set-AzNetworkSecurityGroup]**

7. Associate NSG with Subnet
  - **[Set-AzVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name Subnet-FrontEnd -AddressPrefix "10.0.1.0/24" -NetworkSecurityGroup $nsg]**
  
  - **[$vnet | Set-AzVirtualNetwork]**

8. Display Results
  - **[Get-AzVirtualNetwork -Name VNet-Secure -ResourceGroupName RG-SecureNet]**
  
  - **[Get-AzNetworkSecurityGroup -Name NSG-FrontEnd -ResourceGroupName RG-SecureNet | Get-AzNetworkSecurityRuleConfig]**











