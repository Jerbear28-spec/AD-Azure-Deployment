<p align="center">
<img width="219" height="147" alt="50" src="https://github.com/user-attachments/assets/35714237-f7e3-4855-9df9-7942df66ded7" />
</p>

<h1 align="center">Creating an Active Directory Domain Using Microsoft Azure Vitual Machines</h1>

<h2 align="center">Project Overview</h2>
This tutorial outlines the implementation of an Active Directory domain using Azure virtual machines. In this lab, a virtual machine running Windows Server 2022 will be created and used as a Domain Controller. A Windows 10 virtual machine will be created and used as a "client" for this Active Directory deployment. User accounts will be created and managed on the Domain Controller, and these accounts will be able to login on this client virtual machine. This tutorial will assume a basic understanding of the Microsoft Azure Portal. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Cloud Computing Platform)
- Remote Desktop
- Active Directory Domain Services
- PowerShell (used for account generation)

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>Deployment and Configuration Overview</h2>

- Step 1: Creation of Active Directory Infrastructure
- Step 2: Deployment of Active Directory on Domain Controller
- Step 3: User Account Creation 
- Step 4: Group Policy and Account Management

<h2>Step 1: Creation of Active Directory Infrastructure</h2>

<h3>Create Resource Group</h3>
<p>The first step will be to create a resource group within an Azure subscription. This resource group will be the container for everything in this project. The name for the resource group in this tutorial will be "Active_Directory_Deployment".</p>

<p align="center">
<img width="760" height="381" alt="RGCreation" src="https://github.com/user-attachments/assets/c80a7818-cc83-4e68-a150-c8e5ba947d92" />
</p>

<h3>Create Virtual Network</h3>
<p>Within this new resource group, create a virtual network. Microsoft Azure provides optional paid security services for their virtual networks. These will not be necessary for the purposes of this tutorial. Azure alsp provides configuration settings for the address space of these networks. The default settings will be sufficient.</p>

<p align="center">
  <img width="767" height="652" alt="Vnetcreate" src="https://github.com/user-attachments/assets/57014ce9-a8ed-480c-9611-bcce72d836c1" />
</p>

<h3>Create Domain Controller</h3>
<p>The next step will be to create a virtual machine that will be used as the Domain Controller. </p>

<h3>Create Client Virtual Machine</h3>
<p>ABC</p>

<h2>Step 2: Deployment of Active Directory on Domain Controller</h2>

<h2>Step 3: User Account Creation</h2>

<h2>Step 4: Group Policy and Accont Management</h2>
