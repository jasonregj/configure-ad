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
If you seach for an go straight to Virtual Machines to create a Virtual Machine, it will automatically create a Resource Group for the VM. So we'll start there. 
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
We will also create the guest/user VM simulating an external user logging into the directory. We'll call this VM "Client-1" and it will be on a Windows 10 with at least 2 vcups. We'll use the same username 'labuser' and password for simplicity.
</p>
<p>
<img src="https://i.imgur.com/fHX7ziX.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/W4Ehh4S.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Make sure the virtual network for the Client-1 VM is the same as for the DC-1 VM. For this example the Virtual Network is 'AD-Lab-Vnet.' As your CLient-1 VM is creating, let's change the Networking Interface Controller (NIC) from 'dynamic' to 'static' for the Domain Controller VM. This means whether we turn off the desktop/unplug, the IP Configuration will not change for that server at all. Go to the DC-1 VM -> Networking -> "Networking Interface: dc1164 -> IP Configurations -> Select the IP configuration at bottom -> Click toggle from 'Dynamic' to 'Static' and then click 'Save.'
</p>
<p>
<img src="https://i.imgur.com/oamh45x.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/fk1cFq4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/9hyjEuE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/rXsvrRE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
What we have now done is created a Virtual desktop computer with a Virtual network (separate from our actual computer), a network security group (NSG or firewall), a network interface card (NIC or virtual ethernet port), a public IP address, and a storage disk. For the osTicket demonstrations, we can now login as an administrator in one computer/network and a user in the other virtual computer/network (or vice versa), test connectivity between the networks, and confirm configurations of roles, departments, agents, teams, users, SLAs, and ensure help topics are in place via an admin and a user. Now we will create a second Virtual Machine using Windows Server 22 instead of Windows 10. This will simulate an admin logging in using a Active Directory Domain Server versus a guest user logging into an organizational portal from an external computer. When you get to the the Network page of the second virtual machine, make sure the Vnet is the same as the ADLab02 Vnet. 
<p> 
<br />

<h2>Create a second VM to represent external guest/user</h2>

<p>
Use the same Resource Group.
</p>
<p>
<img src="https://i.imgur.com/m2m7ppf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create an Azure Virtual Machine Windows Server 22, 4 vCPUs
</p>
<p>
- Name the VM 'ADLab02'
</p>
<p>
- Username: 'jasonregj' amd choose a password
</p>

<p>
<img src="https://i.imgur.com/EUL1Qbz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/IqIVw9f.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Once you click the create button for your VM, you can view all the resources within the VM under the Resource Group "VMs_Lab02."
</p>
<p>
<img src="https://i.imgur.com/4hzXbO9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
