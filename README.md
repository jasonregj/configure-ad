<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used</h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1
- Step 2
- Step 3
- Step 4

<h2>Deployment and Configuration Steps</h2>

<p>
If you seach for and go straight to Virtual Machines to create a Virtual Machine, it will automatically create a Resource Group for the VM. So we'll start there. 
</p>

<p>
Create an Azure Virtual Machine Windows 2022 Server (for most updated version), 2 vCPUs
</p>
<p>
- This VM serves as the Domain Controller VM so we'll name it "DC-1." 
</p>
<p>
- Username: 'labuser' amd choose a password
</p>

<p>
<img src="https://i.imgur.com/WousP8v.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/ApcoWhJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
We will also create the guest/user VM simulating an external user logging into the directory. We'll call this VM "Client-1" and it will be on a Windows 10 with at least 2 vcpus. We'll use the same username 'labuser' and password for simplicity.
</p>
<p>
<img src="https://i.imgur.com/fHX7ziX.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/W4Ehh4S.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Make sure the virtual network for the Client-1 VM is the same as for the DC-1 VM. For this example the Virtual Network is 'AD-Lab-Vnet.' As your Client-1 VM is creating, let's change the Networking Interface Controller (NIC) from 'dynamic' to 'static' for the Domain Controller VM. This means whether we turn off the desktop/unplug, the IP Configuration will not change for that server at all. Go to the DC-1 VM -> Networking -> "Networking Interface: dc1164 -> IP Configurations -> Select the IP configuration at bottom -> Click toggle from 'Dynamic' to 'Static' and then click 'Save.'
</p>
<p>
<img src="https://i.imgur.com/oamh45x.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/fk1cFq4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/k5ScTLK.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/9hyjEuE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
We now have two virtual machines to simulate the Domain Controller (Admin Capabilities) and Client (user) where we can simulate managing access control, password resets, file-sharing/permissions, etc. as well as see the impact on the user side of Active Directory software capability. 
</p> 
<br />

<h2>Deploy Active Directory</h2>

<p>
Now that we have both VMs created, we'll remote desktop login to both and test connectivity for both by opening the Windows Command Prompt and "ping" the private IP of DC-1 from Client 1 by typing 'ping -t 10.2.0.4' (DC-1's private IP address).
</p>

<p>
<img src="https://i.imgur.com/4IoFAOf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
We see that we get a "timed out" response which means DC-1's firewall settings have disabled ICMP. We can go to DC-1's "Windows Defender Firewall" and enable pinging by enabling in and outgoing ICMP messaging. 
<p>
<img src="https://i.imgur.com/LqTMz8S.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Ping DC-1 from Client 1 again. This time you shoud see ping success with 4 messages sent and 0 dropped. 
<p>
<br />
  
<p>
Now let's install Active Directory on DC-1. Open Server Manager from the Start button on DC-1 and select 'Add Roles and Features'.
</p>

<p>
<img src="https://i.imgur.com/vn2H5J1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
An install prompt will appear. Hit next until you get to the 'Server Roles' step in the install process. Check the box that says 'Active Directory Domanin Servers -> Next -> Install. 
<img src="https://i.imgur.com/Kf8O0rx.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p> Check the top right alert horn icon on the server manager for a yellow exclamation. Click there and click 'Promote the server to a domain controller.'
<p>
<p>
<img src="https://i.imgur.com/wugJ6r5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>    
<p>
Now a configuration window pops up. Select the bubble 'Add a new forest' and choose a domain name. We will choose 'mydomain.com' for this example. Click next then type in a password. Click next until you get to the 'Installation' step and click 'Install'. Once the installation is complete, the configuration wizard will inform you that the installation is complete and the computer must restart. It may do so automatically. Restart the Remote Desktop for DC-1. Now when we log back in, we must log in with the context of the domain server so we will login with username 'mydomain.com\labuser' and the password we created when we added the forest. Now we have logged in as DC-1 AD DS-enabled.  
</p>
<p>
<img src="https://i.imgur.com/qrQiDG6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/nNUJTxs.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/ZqVby7Z.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/pOj4doN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<h2>Create an Admin and Normal User Account in AD</h2>

<p>
Now we are logged back in DC-1 with AD DS admin capability. Open Active Directory by clciking the start menu. Type Active Directory into the search and click the 'Active Directory Users and Computers' application. This will bring us to the AD User Interface (UI). From here we going to create user accounts. Go to the 'mydomain' drop-down tab. Right click -> New -> Organizational Unit. Name this group '_EMPLOYEES.' I like to use all-caps when I create new folders not defaulted in the domain to help me distinguish what I added to the UI. 
</p>              
<p>
<img src="https://i.imgur.com/nXHRnAp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/SQYU4B2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>                                                                                                 
<br />
                                                                                                 
<p>
We will create an admin organizational unit as well and name it 'ADMINS.'  
</p>
<p>
<img src="https://i.imgur.com/qHIdEnK.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p> 
Right click the ADMINS folder. Hover the mouse over 'New' and click 'User.' From here we are going to create the Admin User 'Jane Doe.' Fill out the information. Jane's domain name will be 'jane_admin.' Click next.
</p>
<p>
<img src="https://i.imgur.com/IFq40wq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p> 
<br/>
                                                                                                 
<p>
Create a password for Jane Doe. We're going to check the 'password never expires' boxe for this example. Click next. Click Finish. Now double-click _ADMINS -> Jane Doe. Right click Jane Doe and select 'Properties.' Click the 'Member of' folder. Here we're going to add user Jane Doe to the member folder 'Domain Admins.' Every member of this group will have admin control and permissions going forward within AD DS. If you type 'Domain' and then click 'Search Groups,' 'Domain Admin' is an option. Click 'Domain Admins' then click 'OK'. Now click 'Apply' and then 'OK.' We have now just created an Admin User account in Active Directory. You can close out of the 'labuser' account and now log in as 'mydomain.com\jane_admin' and the password you created. 
</p>
<br />

<p>
<img src="https://i.imgur.com/eMJOgRn.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/ZqZq4QJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/ArmZWGG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/Cyo4vG6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/CPCexT1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
                                                             
<p>
Now we're going to join Client-1 to our domain (mydomain.com). Copy DC-1's private IP address from Microsoft Azure. Go to Client-1's VM configuration. Go to 'DNS Servers' -> Click 'Client 1138' -> Change the bubble from 'inherit from vitrual network' to 'Custom' and paste the private IP address from DC-1. Click 'Save.' Now restart your remote desktop connection from Client-1. Log back into Client one with 'Labuser' and password originally created for the VM from Azure since we are not quite yet joined to the network. 
</p>
<p>
<img src="https://i.imgur.com/UbJbd1b.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Once we're logged into Client-1, go to Start and go to 'Settings' -> 'Rename this PC (advanced)' -> 'Change' -> Select 'Domain' and type in 'mydomain.com' then select 'OK'. A login will prompt and you can now enter the admin login credentials we created for Jane Doe. So what this means is we have created an external desktop from the AD DS to login with Active Directory admin/user access. 
</p>
<p>
<img src="https://i.imgur.com/sHYHwCH.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<h2>Reset Passwords & Manage User Accounts</h2>

<p>
Let's say a user logs in incorrectly too many time and gets locked out of their account. What we can do as an admin is go to ur AD UI and in the _EMPLOYEES folder, find the user account. For this example we created a 'bet.jax' user and they attempted failed to log in six times and are now locked out after discovering their correct user/pass. Right click 'bet.jax' and click 'Properties'. Click the 'Account' tab and check the 'Unlock Account' box and click 'OK'. That's it. 
</p>
<p>
<img src="https://i.imgur.com/k6xLzh6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/dsKCAJz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Now let's say a user has forgotten their login password and needs a new one. As an admin, you can reset their password and set a temporary password for them where they will be prompted to log in with the temporary password in order to change their password. You can go to the same UI -> _EMPLOYEES -> Right click 'bet.jax' -> Reset password -> Enter new password and click 'OK'. If you noticed, you can also disable an account. This may be the case if an employee leaves the organization and no longer requires organizational access. Upon clicking 'disable account' the login credentials for that user account become invalid. 
</p>
<p>
<img src="https://i.imgur.com/BVlCCQq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/qQTm846.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
