
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This walkthrough outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />



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
- Step 2 Ensure Connectivity between the client and Domain Controller
- Step 3 Install Active Directory
- Step 4 Create an Admin and Normal User Account in AD
- Step 5 Join Client-1 to your domain (mydomain.com)
- Step 6 Setup Remote Desktop for non-administrative users on Client-1
- Step 7 Create a bunch of additional users and attempt to log into client-1 with one of the users

<h2>Deployment and Configuration Steps</h2>

<p>

</p>
<p>
1.) Setup Resources in Azure
Create the Domain Controller VM (Windows Server 2022) named “DC-1”.
Take note of the Resource Group and Virtual Network (Vnet) that get created at this time.
<p>
<img src="https://i.imgur.com/5GZ2did.png" height="50%" width="50%" alt="Intall Windows Server Virtual Machine"/>

<p>
Set Domain Controller’s NIC Private IP address to be static. 
 
<p>
<img src="https://i.imgur.com/pEatsVd.png" height="50%" width="50%" alt="Set Domain Controller NIC"/>
</p>

<br />
Create the Client VM (Windows 10) named “Client-1”. Use the same Resource Group and Vnet that was created in Step 1.a .
Ensure that both VMs are in the same Vnet (you can check the topology with Network Watcher).
<p>
<img src="https://i.imgur.com/w2DaBHa.png" height="50%" width="50%" alt="Diagram"/>
</p>
<p>
</p>
<br /><img src="https://i.imgur.com/XUhBNe0.png" height="50%" width="50%" alt="Set Domain Controller NIC"/>
2.) Ensure Connectivity between the client and Domain Controller.
Login to Client-1 with Remote Desktop and ping DC-1’s private IP address with ping -t <ip address> (perpetual ping).
<p>
<img src="https://i.imgur.com/JRwMqHb.png" height="50%" width="50%" alt="Ping Domain Controller"/>
 
Login to the Domain Controller and enable ICMPv4 in on the local windows Firewall.
Check back at Client-1 to see the ping succeed.
</p>
<br />
<img src="https://i.imgur.com/4tanhzu.png" height="50%" width="50%" alt="Enable ICMPv4"/>
</p>
<br />
3.) Install Active Directory
Login to DC-1 and install Active Directory Domain Services.
</p>
<img src="https://i.imgur.com/8OU2aab.png" height="50%" width="50%" alt="Install AD Domain Services"/>

</p>
<br />
Configure domain controller
Promote as a DC: Setup a new forest as mydomain.com (can be anything, just remember what it is).
Restart and then log back into DC-1 as user: mydomain.com\labuser (important to use the fully qualified domain name).
</p>
<img src="https://i.imgur.com/Bzf7MHy.png" height="50%" width="50%" alt="Configure Domain Controller"/>

</p>
4.) Create an Admin and Normal User Account in AD.
In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”.
<img src="https://i.imgur.com/qVemn3m.png" height="50%" width="50%" alt="Create an Admin and User Account in AD"/>
<img src="https://i.imgur.com/faUm5ZC.png" height="50%" width="50%" alt="Create organizational unit"/>
</p>
Create user, Jane_Admin.
</p> 
<img src="https://i.imgur.com/bKrpaFQ.png" height="50%" width="50%" alt="Create User"/>


</p> 
<img src="https://i.imgur.com/IET78Do.png" height="50%" width="50%" alt="Add User to Group"/>

Add user Jane_Admin to ADIMINS user group.
</p>
Login to DC-1 as jane_admin.
</p>
<img src="https://i.imgur.com/LgaoPEM.png" height="50%" width="50%" alt="Join Client-1 to domain"/>

5.) Join Client-1 to your domain (mydomain.com).

<img src="https://i.imgur.com/4RAwMbg.png" height="50%" width="50%" alt="Set Client DNS to private IP"/>
 </p>
From the Azure Portal, set Client-1’s DNS settings to the DC’s Private IP address.
</p>
From the Azure Portal, restart Client-1.
Login to Client-1 (Remote Desktop) as the original local admin (labuser) and join it to the domain (computer will restart).
</p> 
<img src="https://i.imgur.com/XiO7kXc.png" height="50%" width="50%" alt="join Client-1 to domain"/>
</p> 
From the Azure Portal, restart Client-1.
</p> 
6.) Login to Client-1 (Remote Desktop) as the original local admin (labuser) and join it to the domain (computer will restart).
<img src="https://i.imgur.com/p5723Ei.png" height="50%" width="50%" alt="Enable domain users to use RDP"/>
</p> 
Enable domain users to use remote desktop.
</p> 
<img src="https://i.imgur.com/Hz3rpDj.png" height="50%" width="50%" alt="Verify Client-1 shows up in AD Users and Computers"/>

Login to the Domain Controller (Remote Desktop) and verify Client-1 shows up in Active Directory Users and Computers (ADUC) inside the “Computers” container on the root of the domain.
</p> 
<img src="https://i.imgur.com/6UKEUYG.png" height="50%" width="50%" alt="Create additional users"/>
</p> 
7.) Create a bunch of additional users and attempt to log into client-1 with one of the users.
Login to DC-1 as jane_admin
Open PowerShell_ise as an administrator.
Create a new File and paste the contents of the script into it (https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1)
<img src="https://i.imgur.com/z19cEag.png" height="50%" width="50%" alt="Observe additional users"/>
</p> 
Run the script and observe the accounts being created.
<img src="https://i.imgur.com/bvXvtLq.png" height="50%" width="50%" alt="log into client-1 with new user created"/>
</p> 
Log into Client-1 with one of the accounts (take note of the password in the script).

</p>

Finished!!
