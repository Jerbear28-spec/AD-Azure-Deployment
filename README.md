<p align="center">
<img width="219" height="147" alt="50" src="https://github.com/user-attachments/assets/35714237-f7e3-4855-9df9-7942df66ded7" />
</p>

<h1 align="center">Creating an Active Directory Domain Using Microsoft Azure Virtual Machines</h1>

<h2 align="center">Project Overview</h2>
This tutorial outlines the implementation of an Active Directory domain within Azure virtual machines. In this lab, a virtual machine running Windows Server 2022 will be created and used as a Domain Controller. A Windows 10 virtual machine will be created and used as a "client" for this Active Directory deployment. User accounts will be created and managed on the Domain Controller, and these accounts will be able to login on this client virtual machine. This tutorial will assume a basic understanding of the Microsoft Azure Portal. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Cloud Computing Platform)
- Remote Desktop
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>Deployment and Configuration Overview</h2>

- Step 1: Creation of Active Directory Infrastructure
- Step 2: IP Address Configuration
- Step 3: Deployment of Active Directory on Domain Controller
- Step 4: Account Creation

<h2 align="center">Step 1: Creation of Active Directory Infrastructure</h2>

<h3 align="center">Create Resource Group</h3>
<p align="center">The first step will be to create a resource group within an Azure subscription. This resource group will be the container for everything in this project. The name for the resource group in this tutorial will be "Active_Directory_Deployment".</p>

<p align="center">
<img width="760" height="381" alt="RGCreation" src="https://github.com/user-attachments/assets/c80a7818-cc83-4e68-a150-c8e5ba947d92" />
</p>

<h3 align="center">Create Virtual Network</h3>
<p align="center">Within this new resource group, create a virtual network. Microsoft Azure provides optional paid security services for their virtual networks. These will not be necessary for the purposes of this tutorial. Azure also provides configuration settings for the address space of these networks. The default settings will be sufficient.</p>

<p align="center">
  <img width="767" height="652" alt="Vnetcreate" src="https://github.com/user-attachments/assets/57014ce9-a8ed-480c-9611-bcce72d836c1" />
</p>

<h3 align="center">Create Domain Controller</h3>
<p align="center">The next step will be to create a virtual machine that will be used as the Domain Controller. This VM will be named "DC-1" and will be added to the resource group.</p>

<p align="center">
  <img width="774" height="693" alt="DC1create" src="https://github.com/user-attachments/assets/2fdd7db7-16da-4f4b-b696-a0e96c086e84" />
</p>

<p align="center">For the image, select 'Windows Server 2022 Datacenter: Azure Edition'. Use the specs recommended by the publisher.</p>

<p align="center">
  <img width="771" height="64" alt="DC1image" src="https://github.com/user-attachments/assets/200b28e6-78fb-4e90-a072-01527fecb599" />
</p>

<p align="center">A username and password will need to be created for the admin account. Do not forget these credentials, as they will be crucial to this setup.</p>

<p align="center">
  <img width="762" height="248" alt="DC1adminacct" src="https://github.com/user-attachments/assets/f707a076-00e8-44e6-8b9b-f45ab2e98ffb" />
</p>

<p align="center">Allow connections to this VM through port 3389. This will allow remote connection to this VM. Later, this setting will be changed to only allow RDP traffic from trusted IP addresses (ie. your personal machine).</p>

<p align="center">
  <img width="767" height="273" alt="DC1portrules" src="https://github.com/user-attachments/assets/36720fbd-28ba-4e7b-a2dd-696c8cf664c9" />
</p>

<p align="center">The network will need to be set to the virtual network that was created earlier. The subnet configuration can be left with the default settings.</p>

<p align="center">
  <img width="755" height="183" alt="DC1network" src="https://github.com/user-attachments/assets/fe5d9229-03be-44f7-bc8a-40239abb4acd" />
</p>

<h3 align="center">Create Client Virtual Machine</h3>
<p align="center">Create a new virtual machine, place it in the same resource group, and label it appropriately.</p>

<p align="center">
<img width="841" height="512" alt="clientcreate" src="https://github.com/user-attachments/assets/b4122312-488a-4fd4-bf75-d2a1eaacd1d4" />
</p>

<p align="center">For the image, choose Windows 10 Pro. Use one of the VM sizes recommended by the image publisher.</p>

<p align="center">
<img width="752" height="255" alt="clientimageandsize" src="https://github.com/user-attachments/assets/d181e417-ac0b-405e-b8d1-cbe64517ad23" />
</p>

<p align="center">Use the same admin credentials that were used for the domain controller. Leave the default port rules to provide access to the VM.</p>

<p align="center">
<img width="774" height="517" alt="clientadminportrules" src="https://github.com/user-attachments/assets/88982b0d-8274-4863-9410-2841dca08c0b" />
</p>

<p align="center">For the virtual network, select the one that was created earlier. The subnet configuration should be the same.</p>

<p align="center">
<img width="756" height="103" alt="clientvnet" src="https://github.com/user-attachments/assets/87c24f7c-792c-472a-948e-aabc3e588381" />
</p>

<h3 align="center">Securing RDP Traffic</h3>

<p align="center">By default, these virtual machines will have port 3389 open to the internet. Within Azure, the traffic to this port can be restricted to only allow connections from specific IP addresses. To do this, Click on the VM within Azure and navigate to Network Settings.</p>

<p align="center">
<img width="280" height="537" alt="c1" src="https://github.com/user-attachments/assets/441d2feb-1807-4ab3-905c-1e9b45196545" />
</p>

<p align="center">Within the Network Security Group, click on the rule labeled "RDP". This is the rule that leaves RDP traffic open to the internet.</p>

<p align="center">
<img width="828" height="388" alt="c2" src="https://github.com/user-attachments/assets/4172bfe4-7dd0-437d-8ad4-b0b13ffe43e7" />
</p>

<p align="center">Change the Source IP address to "My IP Address". This will limit the RDP traffic to only allow connections from the PC you're using. Be sure to click "Save" at the bottom to apply this new rule. Repeat this process for the other VM.</p>

<p align="center">
<img width="567" height="364" alt="c3" src="https://github.com/user-attachments/assets/10c37b19-2ae7-4e8c-973b-7c9b951a46d9" />
</p>

<h2 align="center">Step 2: IP Address Configuration</h2>

<h3 align="center">Change Domain Controller's Private IP Address to "Static"</h3>

<p align="center">In the Azure portal, click on the Domain Controller VM. Navigate to "Network Settings" under the Networking tab. </p>

<p align="center">
<img width="258" height="765" alt="DCsettings" src="https://github.com/user-attachments/assets/2bcf32d5-153d-411f-9a85-72c20fb20aba" />
</p>

<p align="center">Click on the IP configuration for this virtual machine.</p>

<p align="center">
<img width="1050" height="400" alt="Dcsettings2" src="https://github.com/user-attachments/assets/fa372cd2-87c1-4b8b-a7c2-6f297e2f06f6" />
</p>

<p align="center">The default name for the IP configuration should be 'ipconfig1". Click on it to edit the settings.</p>

<p align="center">
<img width="854" height="484" alt="dcsettings3" src="https://github.com/user-attachments/assets/f4ec2870-b17f-4911-b661-f6fe9e3d2cf0" />
</p>

<p align="center">Change the Private IP Addressing settings from "dynamic" to "static." This will keep the Domain Controller's private IP address from changing within the virtual network.</p>

<p align="center">
<img width="566" height="616" alt="dcsettings4" src="https://github.com/user-attachments/assets/b622bd18-ac46-4c04-9c9d-895465cb690a" />
</p>

<h3 align="center">Manually Change the Client Virtual Machines DNS Configuration</h3>

<p align="center">Login to the client PC via Remote Desktop using the client PC's public IP address.</p>

<p align="center">
<img width="351" height="334" alt="clientdns1" src="https://github.com/user-attachments/assets/97924e07-154d-45fb-95b4-f08ba100514c" />
</p>

<p align="center">Navigate to "Network Connections", right click on the ethernet connection, and click "Properties." </p>

<p align="center">
  <img width="1202" height="934" alt="clientdns2" src="https://github.com/user-attachments/assets/d205cc9f-099d-4669-b015-623b4cf4bd82" />
</p>

<p align="center">Click on "Internet Protocol Version 4" and then click properties again.</p>

<p align="center">
  <img width="1202" height="934" alt="clientdns3" src="https://github.com/user-attachments/assets/bde4bc49-37e7-4b59-bb03-013fc72b303a" />
</p>

<p align="center">"Select "Use the following DNS Server Addresses" and manually input the private IP address of the Domain Controller. If the RDP connection drops, the client virtual machine may need to be restarted from the Azure portal.</p>

<p align="center">
  <img width="1202" height="934" alt="clientdns4" src="https://github.com/user-attachments/assets/56d1d5e9-7f67-495b-a448-822a86ec8ce3" />
</p>

<h2 align="center">Step 3: Deployment of Active Directory on Domain Controller</h2>

<p align="center">Use Remote Desktop to connect to Domain Controller and login with the Admin credentials that were created earlier.</p>

<p align="center">
<img width="351" height="334" alt="clientdns1" src="https://github.com/user-attachments/assets/9fa7a74f-1fd3-4858-aa09-531783559cea" />
</p>

<p align="center">The Server Manager dashboard should open automatically after login. This software comes pre-installed on Windows Server 2022. From the dashboard, click on "Add Roles and Features".</p>

<p align="center">
<img width="1202" height="934" alt="deployAD1" src="https://github.com/user-attachments/assets/48a97d33-d7a6-4179-abc6-fb1cd96501a1" />
</p>

<p align="center">Click next on the "Before you begin" page...</p>

<p align="center">
<img width="1202" height="934" alt="deployAD2" src="https://github.com/user-attachments/assets/793bd41f-ca17-4109-b823-28f9383f2be1" />
</p>

<p align="center">For the installation type, select "Role-based or feature-based installation"</p>

<p align="center">
<img width="1202" height="934" alt="deployAD3" src="https://github.com/user-attachments/assets/ed19744c-aeaf-4964-9fd3-744834795c91" />
</p>

<p align="center">For the destination server, select the Domain Controller VM for the installation (there should only be one option.)</p>

<p align="center">
<img width="1202" height="934" alt="deployAD4" src="https://github.com/user-attachments/assets/ed0550ac-d84d-47bc-8ca7-fa93270bc82c" />
</p>

<p align="center">Select "Active Directory Domain Services" in the list of available roles. Click "next", then "Install".</p>

<p align="center">
<img width="1202" height="934" alt="deployAD5" src="https://github.com/user-attachments/assets/7e03e2b3-bb66-4553-b77b-83a97c9b0ac8" />
</p>

<p align="center">Click on the notifications button, then click on "Promote this server to  a domain controller"</p>

<p align="center">
  <img width="1202" height="934" alt="deployAD6" src="https://github.com/user-attachments/assets/fd269dce-d1b2-48de-8fb9-7f68d3a20c1c" />
</p>

<p align="center">For the deployment operation, select "Add a new forest". Then enter in a name for the domain that will be created.</p>

<p align="center">
  <img width="1202" height="934" alt="deployAD7" src="https://github.com/user-attachments/assets/7dac1f19-5af8-4557-9517-aee4f2e531eb" />
</p>

<p align="center">In Domain Controller Options, create a password for the Directory Services Restore Mode. This can be the same password as the Admin account created earlier.</p>

<p align="center">
  <img width="1202" height="934" alt="deployAD8" src="https://github.com/user-attachments/assets/39e3f72a-fce6-49f6-a37b-bf39207e7013" />
</p>

<p align="center">All of the other options can be left with  the default configuration. Once the prerequisite check is complete, select "Install". The Server VM is now officially a Domain Controller for the Active Directory domain.</p>

<p align="center">
  <img width="1202" height="934" alt="deployAD9" src="https://github.com/user-attachments/assets/034e9a7e-a4b8-4381-8a4d-98b6a8d9de30" />
</p>

<h3 align="center">Add Client Virtual Machine to the New Domain</h3>

<p align="center">Connect to the Client VM using Remote Desktop. Navigate to the "About" tab in the settings. Click on "Rename this PC (Advanced)".</p>
<p align="center">
  <img width="1202" height="934" alt="b1" src="https://github.com/user-attachments/assets/6558abf5-540e-45d1-b328-6a0508637aeb" />
</p>

<p align="center">Under the Computer Name tab, click on "Change..."</p>
<p align="center">
  <img width="1202" height="934" alt="b2" src="https://github.com/user-attachments/assets/03971de1-87e8-48b4-a034-df88c81a213b" />
</p>

<p align="center">Select the option to add this VM as a member of the domain that was recently created.</p>
<p align="center">
  <img width="329" height="420" alt="b3" src="https://github.com/user-attachments/assets/30b47f44-56a7-4f21-b359-e145bf222643" />
</p>

<p align="center">Once the Client VM is successfully added to the domain, it must be restarted.</p>
<p align="center">
  <img width="299" height="149" alt="b4" src="https://github.com/user-attachments/assets/1e7df63e-dcb7-46c9-a7bb-d39fe3f62493" />
</p>

<h2 align="center">Step 4: Account Creation</h2>

<h3 align="center">Create an Admin Account within Domain</h3>

<p align="center">Connect to the Domain Controller using Remote Desktop. From the Start menu, navigate to "Active Directory Users and Computers" in the Windows Administrative Tools folder.</p>
<p align="center">
  <img width="962" height="748" alt="a1" src="https://github.com/user-attachments/assets/19902815-7c0a-4629-bf3a-f2043aefb14a" />
</p>

<p align="center">Click on the Domain directory. Within this folder, right-click and create a new "Organization Unit".</p>
<p align="center">
  <img width="962" height="748" alt="a2" src="https://github.com/user-attachments/assets/2d4ba79b-be39-4841-b342-ed35b959b902" />
</p>

<p align="center">Create an appropriate name for a folder for Admin Users. There is an option for protecting this container from accidental deletion.</p>
<p align="center">
  <img width="962" height="748" alt="a3" src="https://github.com/user-attachments/assets/d19a12e3-3bd3-4e11-b344-0d74dbfe9450" />
</p>

<p align="center">Within this new container, right-click and create a new User.</p>
<p align="center">
  <img width="962" height="748" alt="a4" src="https://github.com/user-attachments/assets/0ed17e22-50d5-427c-85bb-13094b8d09a7" />
</p>

<p align="center">Input the information for a new Admin user. The "User logon name" will be used to login to the client VM.</p>
<p align="center">
  <img width="962" height="748" alt="a5" src="https://github.com/user-attachments/assets/51a89c71-a8c0-4b46-adca-b6488b7615dc" />
</p>

<p align="center">Create a password for this user. There are a few options available for this password/account.</p>
<p align="center">
  <img width="962" height="748" alt="a6" src="https://github.com/user-attachments/assets/8f97d0fe-0cd3-4043-84c1-d5b5eb36eaac" />
</p>

<p align="center">In order for the domain to recognize that this user is an Administrator, the user will need to be added to the group, "Domain Admins". To do this, right-click on the user and select "Add to a group..."</p>
<p align="center">
  <img width="962" height="748" alt="a7" src="https://github.com/user-attachments/assets/6f1f55b9-ee22-45db-ba6d-aa6f82e34f3b" />
</p>

<p align="center">Enter the object name, "Domain Admins", click Check Names, then click OK. This will add this user to the domain group and effectively give them Admin permissions. This process can be repeated for different employees by creating different containers / users within the main directory. By creating a User, they are automatically added to the group "Users" and will be able to login to the Client VM using their individual credentials. Attempt to login to the Client VM with the newly created admin user.</p>
<p align="center">
  <img width="962" height="748" alt="a8" src="https://github.com/user-attachments/assets/bd27915d-dc72-4196-b7e5-b259cfa5225f" />
</p>
