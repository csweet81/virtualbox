<p align="center">
<img src="https://i.imgur.com/RLMgzCB.png" alt="VirtualBox logo"/>
</p>

<h1>Setting Up an Active Directory Lab Using VirtualBox</h1>
<p>In this guide, you will create a full Active Directory lab on your personal computer using VirtualBox. This lab will help you understand Active Directory and Windows networking. You can repeat the process multiple times to build intuition and even attempt it without instructions to test your knowledge.</p>

<p>By the end of this lab you'll be able to: 
  
- Manage users in Active Directory.
- Use DHCP and NAT for networking.
- Join computers to a domain.
- Log in with domain credentials.

</p>

<br />

<h2>Environments and Technologies Used</h2>
- Microsoft Active Directory
- VirtualBox

<h2>Operating Systems Used </h2>
- Windows 10 Pro, version 22H2 - x64 Gen2
- Windows Server 2019

<h2>Overview</h2>

- Step 1: Install VirtualBox & Required Software
- Step 2: Create a Virtual Machine for the Domain Controller
- Step 3: Configure the Domain Controller
- Step 4: Install Active Directory & Create a Domain
- Step 5: Configure Additional Services
- Step 6: Bulk Create Users with PowerShell
- Step 7: Create a Windows 10 Client
- Step 8: Join the Client to the Domain
- 

<h2>Windows Virtual Machine Installation Steps</h2>

<img src="https://i.imgur.com/zPw9Kpj.png" height="80%" width="80%" alt="Setting up DC via Virtualbox"/>

<h3> Step 1: Configure Windows Server 2019 (DC) via VirtualBox. </h3>

- 1.1 Click 'New'
- Name it 'DC'
- Choose the version 'Other version (Windows 64-Bit)'
- Click 'Continue'
- Scroll down to System and change Base Memory to 2048 MB
-  



  
</p>
<br />

<p>
<img src="https://i.imgur.com/r6KduZ5.png" height="80%" width="80%" alt="Creating a Resource Group"/>
</p>
<p>
Step 2: Within the Azure portal, create a resource group. This will be used to store the virtual machines and associated files. 
</p>
<br />

<p>
<img src="https://i.imgur.com/mvdcoLE.png" height="80%" width="80%" alt="Create Windows 10 virtual machine"/>
</p>
<p>
Step 3: Create a Windows 10 virtual machine. Ensure that the subscription, resource group, and region options match the resource group you will be using. 

Choose Windows 10 Pro 22H2. The VM architecture should be x64. Your VM size should be at least 2 vcpus to ensure smooth operation. Check the box at the bottom to confirm that you have an eligble Windows 10/11 license.   

Click Review+Create. 

</p>
<p>
<img src="https://i.imgur.com/kZNi51G.png" height="80%" width="80%" alt="Validating deployment"/>
</p>

<p>
If you get an error screen, go back and correct the red-highlighted areas. Once validated, click Create to deploy the Windows 10 virtual machine.   

Click Review+Create. 
</p>

<p>
<img src="https://i.imgur.com/nuOnEk5.png" height="80%" width="80%" alt="Completing Windows VM creation"/>
</p>


<p>
The Windows virtual machine has been successfully deployed!
</p>

<h2>Linux Virtual Machine Installation Steps</h2>

<p>
<img src="https://i.imgur.com/nSMJBRQ.png" height="80%" width="80%" alt="Logging into Microsoft Azure"/>
</p>
<p>
Step 1: Log into the Azure Portal. 
</p>
<br />

<p>
<img src="https://i.imgur.com/r6KduZ5.png" height="80%" width="80%" alt="Creating a Resource Group"/>
</p>
<p>
Step 2: Within the Azure portal, create a resource group. This will be used to store the virtual machines and associated files. 
</p>
<br />

<p>
<img src="https://i.imgur.com/2blEGro.png" height="80%" width="80%" alt="Create Linux virtual machine"/>
</p>
<p>
Step 3: Create a Linux virtual machine. Ensure that the subscription, resource group, and region options match the resource group you will be using. 

Choose Ubuntu Server 22.04. The VM architecture should be x64. Your VM size should be at least 2 vcpus to ensure smooth operation.
Click Review+Create. 

</p>
<p>
<img src="https://i.imgur.com/kZNi51G.png" height="80%" width="80%" alt="Validating deployment"/>
</p>

<p>
If you get an error screen, go back and correct the red-highlighted areas. Once validated, click Create to deploy the Windows 10 virtual machine.   

Click Review+Create. 
</p>

<p>
<img src="https://i.imgur.com/0pUbRUD.png" height="80%" width="80%" alt="Completing Windows VM creation"/>
</p>


<p>
The Linux virtual machine has been successfully deployed!
</p>


<br />
