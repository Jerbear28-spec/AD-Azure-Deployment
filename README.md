<p align="center">
<img width="219" height="147" alt="50" src="https://github.com/user-attachments/assets/35714237-f7e3-4855-9df9-7942df66ded7" />
</p>

<h1 align="center">Creating an Active Directory Domain Using Microsoft Azure Virtual Machines</h1>

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
<p>The next step will be to create a virtual machine that will be used as the Domain Controller. This VM will be named "DC-1" and will be added to the resource group.</p>

<p align="center">
  <img width="774" height="693" alt="DC1create" src="https://github.com/user-attachments/assets/2fdd7db7-16da-4f4b-b696-a0e96c086e84" />
</p>

<p>For the image, select 'Windows Server 2022 Datacenter: Azure Edition'. Use the specs recommended by the publisher of this image.</p>

<p align="center">
  <img width="771" height="64" alt="DC1image" src="https://github.com/user-attachments/assets/200b28e6-78fb-4e90-a072-01527fecb599" />
</p>

<p>A username and password will need to be created for the admin account. Do not forget these credentials, as they are crucial to this setup.</p>

<p align="center">
  <img width="762" height="248" alt="DC1adminacct" src="https://github.com/user-attachments/assets/f707a076-00e8-44e6-8b9b-f45ab2e98ffb" />
</p>

<p>Allow connections to this VM through port 3389. This will allow remote connection to this VM. Later, this setting will be changed to only allow RDP traffic from trusted IP addresses (your personal machine).</p>

<p align="center">
  <img width="767" height="273" alt="DC1portrules" src="https://github.com/user-attachments/assets/36720fbd-28ba-4e7b-a2dd-696c8cf664c9" />
</p>

<p>The network will need to be set to the virtual network created earlier. The subnet configuration can be left with the default settings.</p>

<p align="center">
  <img width="755" height="183" alt="DC1network" src="https://github.com/user-attachments/assets/fe5d9229-03be-44f7-bc8a-40239abb4acd" />
</p>

<h3>Create Client Virtual Machine</h3>
<p>Create a new virtual machine, place it in the same resource group, and label it appropriately.</p>

<p align="center">
<img width="841" height="512" alt="clientcreate" src="https://github.com/user-attachments/assets/b4122312-488a-4fd4-bf75-d2a1eaacd1d4" />
</p>

<p>For the image, choose Windows 10 Pro, and one of the VM sizes recommended by the image publisher.</p>

<p align="center">
<img width="752" height="255" alt="clientimageandsize" src="https://github.com/user-attachments/assets/d181e417-ac0b-405e-b8d1-cbe64517ad23" />
</p>

<p>Use the same admin credentials that were used for the domain controller. Leave the default port rules to provide access to the VM.</p>

<p align="center">
<img width="774" height="517" alt="clientadminportrules" src="https://github.com/user-attachments/assets/88982b0d-8274-4863-9410-2841dca08c0b" />
</p>

<p>For the virtual network, select the one that was created earlier. The subnet configuration should be the same.</p>

<p align="center">
<img width="756" height="103" alt="clientvnet" src="https://github.com/user-attachments/assets/87c24f7c-792c-472a-948e-aabc3e588381" />
</p>

<h2>Step 2: IP Address Configuration</h2>

<h3>Change Domain Controller's Private IP Address to "Static"</h3>

<p>In the Azure portal, click on the Domain Controller VM. Navigate to "Network Settings" under the Networking tab. </p>

<p align="center">
<img width="258" height="765" alt="DCsettings" src="https://github.com/user-attachments/assets/2bcf32d5-153d-411f-9a85-72c20fb20aba" />
</p>

<p>Click on the IP configuration for this virtual machine.</p>

<p align="center">
<img width="1050" height="400" alt="Dcsettings2" src="https://github.com/user-attachments/assets/fa372cd2-87c1-4b8b-a7c2-6f297e2f06f6" />
</p>

<p>The default name for the IP configuration should be 'ipconfig1". Click on it to edit the settings.</p>

<p align="center">
<img width="854" height="484" alt="dcsettings3" src="https://github.com/user-attachments/assets/f4ec2870-b17f-4911-b661-f6fe9e3d2cf0" />
</p>

<p>Change the Private IP Addressing settings from "dynamic" to "static." This will keep the Domain Controller's private IP address from changing within the virtual network.</p>

<p align="center">
<img width="566" height="616" alt="dcsettings4" src="https://github.com/user-attachments/assets/b622bd18-ac46-4c04-9c9d-895465cb690a" />
</p>

<h3>Manually Change the Client Virtual Machines DNS Configuration</h3>

<p>text</p>

<p align="center">
  pic
</p>

<p align="center">
  pic
</p>

<p align="center">
  pic
</p>

<h2>Step 3: User Account Creation</h2>

<h2>Step 4: Group Policy and Accont Management</h2>
