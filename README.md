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
We will use the same steps creating our osTicket configuration for this project. Create your Resource Group in Microsoft Azure (must have a subscription). 
</p>
<p>
<img src="https://i.imgur.com/m2m7ppf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create an Azure Virtual Machine Windows 10, 4 vCPUs
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

<p>
Download Microsoft Remote Desktop from Google. Open the application and copy the public IP address from your VM's Virtual Network and copy it into the Remote Desktop "Add PC" PC Name. You can view this information from Home -> VM-osTicket. Login with username 'jasonregj' and the password created.
</p>
<p>
<img src="https://i.imgur.com/2oKJfXj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/lmeECL3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/fyFZWsy.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Select 'Continue'
</p>
<p>
<img src="https://i.imgur.com/kIuM5jG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/rXsvrRE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
What we have now done is created a Virtual desktop computer with a Virtual network (separate from our actual computer), a network security group (NSG or firewall), a network interface card (NIC or virtual ethernet port), a public IP address, and a storage disk. For the osTicket demonstrations, we can now login as an administrator in one computer/network and a user in the other virtual computer/network (or vice versa), test connectivity between the networks, and confirm configurations of roles, departments, agents, teams, users, SLAs, and ensure help topics are in place via an admin and a user. Now we will create a second Virtual Machine using Windows Server 22 instead of Windows 10. This will simulate an admin logging in using a Active Directory Domain Server versus a guest user logging into an organizational portal from an external computer. When you get to the the Network page of the second virtual machine, make sure the Vnet is the same as the ADLab02 Vnet. 
<p> 
<br />

