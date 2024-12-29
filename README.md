Deploy an Azure VM with Bicep

Author: Alex
Date: 12/25/2024
Description: This document explains how to use the provided Bicep template to deploy a virtual machine (VM) on Microsoft Azure. Bicep offers a declarative approach for defining your Azure infrastructure, making deployments consistent, repeatable, and easier to manage.

Prerequisites
Azure Subscription: An active Azure subscription is required to deploy the VM. If you don't have one, you can sign up for a free trial at https://azure.microsoft.com/en-us/pricing/purchase-options/azure-account.
Azure CLI or PowerShell: You'll need either Azure CLI or Azure PowerShell installed to deploy the Bicep template. Both tools provide functionalities to interact with Azure resources.
Understanding the Bicep Template
This Bicep template defines all the necessary resources for deploying a VM in Azure. Here's a breakdown of the resources involved:

Parameters:

vmName: Name for your virtual machine.
vmSize: Size of the VM (e.g., 'Standard_B2s').
adminUsername: Username for administrative access to the VM (default: 'azureuser').
@secure()adminPassword`: Password for the admin user (marked as secure).
imagePublisher: Publisher of the VM image (e.g., 'Canonical').
imageOffer: Offer of the VM image (e.g., 'UbuntuServer').
imageSku: SKU of the VM image (e.g., '20.04-LTS').
tags: Optional tags to associate with the deployed resources.
Resources:

Virtual Network: Defines a virtual network to isolate your VM from other resources.
Subnet: Creates a subnet within the virtual network for the VM.
Network Security Group (NSG): Defines security rules for inbound and outbound traffic for the VM.
Public IP Address: Provides a public IP address for remote access to the VM (optional, depending on your needs).
Network Interface: Connects the VM to the virtual network and optionally assigns a public IP.
Virtual Machine: Deploys the VM with the chosen configuration, including OS image, hardware size, and network interface.
Security Rule:

The template defines a security rule allowing Remote Desktop Protocol (RDP) access on port 3389 to the VM from anywhere. This allows initial configuration after deployment. You can adjust or remove this rule based on your security requirements.

Deployment Steps
Save the Bicep Template: Save the Bicep template as main.bicep in your local directory.

Update Parameters (Optional): Modify the parameters in the main.bicep file to personalize your deployment.

Deploy the Template: Choose one of the following methods to deploy the Bicep template:

a) Using Azure CLI:

Open a terminal and navigate to the directory containing main.bicep. Run the following command, replacing <resource_group_name>, <vm_name>, <your_password>, and <location> with your values:

Bash

az deployment group create --resource-group <resource_group_name> --template-file main.bicep --parameters vmName=<vm_name> adminPassword=<your_password> location=<location>
b) Using Azure PowerShell:

Open a PowerShell window and navigate to the directory containing main.bicep. Run the following command, replacing the placeholders with your values:

      New-AzResourceGroupDeployment -ResourceGroupName <resource_group_name> -TemplateFile main.bicep -TemplateParameterObject 1  @{vmName="<vm_name>"; adminPassword="<your_password>"; location="<location>"}
```   
 1. 
github.com
github.com

Access the VM (Optional):

If you assigned a public IP address to the VM, you can access it using the assigned IP address and the configured username and password.

Additional Notes:

Remember to store the admin password securely (not in the Bicep file itself).
Consider using Azure Key Vault to manage secrets like passwords for improved security.
This template provides a basic example. You can customize it further by adding additional resources or modifying configurations.
For more advanced deployments, explore resource dependencies and output values in Bicep.
