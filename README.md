<p align="center">
<img src="https://i.imgur.com/nB36QwJ.png" alt="VirtualBox logo"/>
</p>

# **Setting Up an Active Directory Lab Using VirtualBox**

## **Overview**
By the end of this guide you'll be able to: 

- Manage users in Active Directory.
- Use DHCP and NAT for networking.
- Join computers to a domain.
- Log in with domain credentials.

Let's dive in. 

---

## **Step 1: Install VirtualBox & Required Software**
### **1. Download and Install VirtualBox**
- Visit the [VirtualBox website](https://www.virtualbox.org/) and download the appropriate version for your system (Windows, macOS, or Linux).
- Install VirtualBox.

### **2. Download and Install VirtualBox Extension Pack**
- After installing VirtualBox, download the **Extension Pack** from the same website.
- Open VirtualBox, go to **Preferences > Extensions**, and install the Extension Pack.

### **3. Download Windows 10 & Windows Server 2019 ISOs**
- **Windows 10:** Go to Microsoft’s website and download the **Windows 10 ISO**.
  - Choose **Windows 10 (64-bit)**, select your language, and download the ISO.
- **Windows Server 2019:** Download the **Server 2019 ISO** from Microsoft.
  - Select **ISO**, fill in any required details, and download.

---

## **Step 2: Create a Virtual Machine for the Domain Controller**
### **1. Create the VM in VirtualBox**
- Open **VirtualBox**, click **New**.
- Name it **DC** (Domain Controller).
- Set the OS type to **Windows Server 2019 (64-bit)**.
- Assign **2GB RAM** (or more if available).
- Create a **Virtual Hard Disk** (default settings).

### **2. Configure the VM**
- Select the VM, go to **Settings**:
  - **Advanced:**
    - Set **Clipboard** & **Drag and Drop** to **Bi-Directional**.
  - **System > Processor:**
    - Allocate **at least 2 CPU cores** (more if available).
  - **Network:**
    - **Adapter 1**: **NAT** (for internet access).
    - **Adapter 2**: **Internal Network** (for domain communication).

### **3. Install Windows Server 2019**
- Start the VM.
- Select the **Server 2019 ISO** as the boot device.
- Install **Windows Server 2019 with Desktop Experience**.
- Set the **Administrator password to "Password1"**.
- Once installation is complete, log in.

---

## **Step 3: Configure the Domain Controller**
### **1. Install VirtualBox Guest Additions**
- In **VirtualBox**, go to **Devices > Insert Guest Additions CD Image**.
- Open **File Explorer**, navigate to the **CD drive**, and install the **AMD64 version**.
- **Restart the VM** after installation.

### **2. Configure Network Settings**
- Open **Network Settings** in the VM.
- Identify the **Internal Network Adapter** (it will have a **169.254.x.x address**).
- Rename the adapters:
  - **"Internet"** for the **NAT adapter**.
  - **"Internal"** for the **internal network adapter**.
- Assign a **Static IP Address** to the **Internal Adapter**:
  - IP Address: 172.16.0.1
  - Subnet Mask: 255.255.255.0
  - Default Gateway: (Leave Blank)
  - Preferred DNS Server: 127.0.0.1 (Loopback)

### **3. Rename the Server**
- Go to **System Properties**, rename the PC to **DC**, and restart.

---

## **Step 4: Install Active Directory & Create a Domain**
### **1. Install Active Directory Domain Services**
- Open **Server Manager > Add Roles and Features**.
- Select **Active Directory Domain Services** and install it.

### **2. Promote to Domain Controller**
- After installation, click the **flag icon** in Server Manager.
- Choose **Add a new forest**, set **Domain Name**:
  - mydomain.com
- Use **Password1** for the Directory Services Restore Mode (DSRM) password.
- Complete the installation and **restart**.

---

## **Step 5: Configure Additional Services**
### **1. Set Up NAT for Internet Access**
- Open **Server Manager > Add Roles and Features**.
- Install **Remote Access > Routing**.
- Open **Routing and Remote Access**, enable **NAT** on the **Internet adapter**.

### **2. Configure DHCP for Clients**
- Install **DHCP Server** from **Server Manager**.
- Open **DHCP Management**, create a new **Scope**:
  - Scope Name: Internal DHCP IP Range: 172.16.0.100 - 172.16.0.200
  - Subnet Mask: 255.255.255.0 Default
  - Gateway: 172.16.0.1
  - (Domain Controller) Preferred DNS Server: 172.16.0.1
- Activate the scope and restart the **DHCP service**.

---

## **Step 6: Bulk Create Users with PowerShell**
### **1. Download the [PowerShell Script](https://drive.google.com/file/d/1hkAzwuC1C7f0OUyJ-8IwRFnUqpTQkqFa/view?usp=drive_link)**
- Disable **Internet Explorer Enhanced Security** in **Server Manager**.
- Download the script from the provided link.
- Extract it to the **Desktop**.

### **2. Modify & Run the Script**
- Open **PowerShell ISE as Administrator**.
- Set execution policy:  
```powershell
Set-ExecutionPolicy Unrestricted -Force

Open the script, edit names.txt, adding your own name at the top.
Run the script to create 1,000 user accounts.
```
## **Step 7: Create a Windows 10 Client**
### **Create the VM**
- In VirtualBox, click New.
  - Name it Client1, select Windows 10 (64-bit).
  - Allocate 4GB RAM (if possible).
  - Assign an Internal Network Adapter.
  - Install Windows 10.
- Verify DHCP & Internet
  - Open Command Prompt, type:
    - ipconfig
- Ensure an IP in the 172.16.0.x range and a default gateway of 172.16.0.1.
- Test internet access with:
  - ping google.com
 
## **Step 8: Join the Client to the Domain**

### **1. Rename the Computer & Join the Domain**
- Open **System Properties** and click **Change**.
- Rename the computer to **Client1**.
- In the **Domain field**, enter:
  - mydomain.com
- Provide your **domain admin credentials** when prompted.
- Restart the virtual machine (VM).

### **2. Log In with a Domain User**
- On the login screen, select **Other User**.
- Sign in using your **domain username**, e.g.'FLNAME'
- Enter the password 'Password1'
- Wait for the **user profile** to be created.
 
  
 





 

