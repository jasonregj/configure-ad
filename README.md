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
Now that we have both VMs created, we'll remote desktop login to both and test connectivity for both by opening the Windows Command Prompt and "ping" the private IP of DC-1 from Client 1 by typing 'ping -t 10.2.0.4 (DC-1's private IP address).
</p>

<p>
<img src="https://i.imgur.com/4IoFAOf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
We see that we get a "timed out" response which mean DC-1's firewall settings have disabled ICMP. We can go to DC-1's "Windows Defender Firewall" and enable pinging by enabling in and outgoing ICMP messaging. 
<p>
<img src="https://i.imgur.com/LqTMz8S.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Now let's install Active Directory on DC-1.
<p>
<br />
  
<p>
Now let's install Active Directory. Open Server Manager from the Start button on DC-1 and select 'Add Roles and Features'.
</p>

<p>
<img src="https://i.imgur.com/vn2H5J1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
An install prompt will appear. Hit next until you get to the 'Server Roles' step in the install process. Check the box that says 'Active Directory Domanin Servers -> Next -> Install. 
<img src="https://i.imgur.com/Kf8O0rx.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
