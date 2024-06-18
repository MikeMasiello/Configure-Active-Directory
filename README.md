
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

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1 Setup Resources in Azure
- Step 2
- Step 3
- Step 4

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/5GZ2did.png" height="80%" width="80%" alt="Intall Windows Server Virtual Machine"/>
</p>
<p>
Create the Domain Controller VM (Windows Server 2022) named “DC-1”
Take note of the Resource Group and Virtual Network (Vnet) that get created at this time

</p>
<br />

<p>
<img src="https://i.imgur.com/pEatsVd.png" height="80%" width="80%" alt="Set Domain Controller NIC"/>
</p>
<p>Set Domain Controller’s NIC Private IP address to be static
</p>
<br />
<img src="https://i.imgur.com/XUhBNe0.png" height="80%" width="80%" alt="Set Domain Controller NIC"/>

<p>
<img src="https://i.imgur.com/w2DaBHa.png" height="80%" width="80%" alt="Diagram"/>
</p>
<p>
Create the Client VM (Windows 10) named “Client-1”. Use the same Resource Group and Vnet that was created in Step 1.a 
Ensure that both VMs are in the same Vnet (you can check the topology with Network Watcher
</p>
<br />
<img src="https://i.imgur.com/JRwMqHb.png" height="80%" width="80%" alt="Ping Domain Controller"/>
Ensure Connectivity between the client and Domain Controller
Login to Client-1 with Remote Desktop and ping DC-1’s private IP address with ping -t <ip address> (perpetual ping)
</p>
<br />

<img src="https://i.imgur.com/4tanhzu.png" height="80%" width="80%" alt="Enable ICMPv4"/>
</p>
<br />
Login to the Domain Controller and enable ICMPv4 in on the local windows Firewall
Check back at Client-1 to see the ping succeed
</p>
<br />

<img src="https://i.imgur.com/8OU2aab.png" height="80%" width="80%" alt="Install AD Domain Services"/>
Install Active Directory
Login to DC-1 and install Active Directory Domain Services
</p>
<br />
<img src="https://i.imgur.com/Bzf7MHy.png" height="80%" width="80%" alt="Configure Domain Controller"/>
Configure domain controller
Promote as a DC: Setup a new forest as mydomain.com (can be anything, just remember what it is)
Restart and then log back into DC-1 as user: mydomain.com\labuser (important to use the fully qualified domain name)


Create an Admin and Normal User Account in AD
In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”

