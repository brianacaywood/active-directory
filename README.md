# Active-Directory
Creating a domain controller, deploying, and demonstarting Active Directory
<p align="center">
<img src="https://jumpcloud.com/wp-content/uploads/2016/07/AD1.png" alt="VPN Usage"/>
</p>

<h1>Installing and demonstrating Microsoft Active Directory </h1>
In this tutorial, we create a server virtual machine and a client virtual machine to deploy and demonstrate how Active Directory is utilized. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Computer)
- Windows Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Windows 10 Server

<h2>Actions and Observations</h2>

<p>
<img src="https://user-images.githubusercontent.com/131008349/233227592-a293f528-7a9d-4d65-9662-7e6e50f4e8a4.PNG" height="80%" width="80%" alt="Create subscription in Azure"/>
</p>
<p>
Login to Portal.Azure.com and create a VM but instead of using Windows 10 (21H2), you will use the Windows 10 Server for the imaging. Keep in mind the login credentials for each of the VM's.
</p>
<br />

<p>
<img src="https://user-images.githubusercontent.com/131008349/233227735-e30727e1-1a7a-4c2f-ab27-912a8e2a7cb9.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create a client VM using the Windows 10 imaging that will access the domain controller later. 
</p>
<br />

<p>
<img src="https://user-images.githubusercontent.com/131008349/233228173-b68868df-571a-4856-94e1-e2d3117274ab.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In the client VM, access the command line to attempt to ping the Domain Controller. Observe that because we have not made the IP address static for the Domain Controller to make the IP address reliably discoverable over the network and we're receiving no reply from the Domain Controller.
</p>
<br />

<p>
<img src="https://user-images.githubusercontent.com/131008349/233228334-96cae009-d919-4bb4-bb0f-4af334397213.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Make the Domain Controller IP address static in Azure by going to the VM that you made the Windows Server, locating "Networking"in the action menu, click the "Network interface", then under the settings click "IP Configurations" then click the private IP address and change it from "Dynamic" to "Static". 
</p>
<br />

<p>
<img src="https://user-images.githubusercontent.com/131008349/233230521-2f79cc75-2899-4b53-ba39-e8796e4cfc75.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Copy the Domain Controller public IP address and remote into the server VM using Remote Desktop Connection. 
</p>
<br />

<p>
<img src="https://user-images.githubusercontent.com/131008349/233231605-3a40e585-9ceb-4142-bb21-8e28904fdfcd.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Once logged in, right click the start menu and type "control". Click "System Security", then "Windows Firewall Defender". On the left side action menu select "Advanced Settings". Click "Inbound Rules" in the left side action menu and sort by "Protocol". Enable all ICMP4 protocols.
</p>
<br />

<p>
<img src="https://user-images.githubusercontent.com/131008349/233231815-f1e2c1a1-4621-4835-a4e3-ee8af4abb892.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Perpetually ping Domain Controller private after enabling ICMP4 in the client VM. Observe there is now a reply.  
</p>
<br />

<p>
<img src="https://user-images.githubusercontent.com/131008349/233231965-7665c02c-8751-4ee4-84da-21752d59c9e5.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Add roles and features in the server manager of the Domain Controller and add Active Directory Domain Services. 
</p>
<br />

<p>
<img src="https://user-images.githubusercontent.com/131008349/233232406-86971e73-3191-4c7e-adbb-defc9117a943.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next through prerequisites and finish install. 
</p>
<br />

<p>
<img src="https://user-images.githubusercontent.com/131008349/233232666-b82ffe00-454b-4fe7-b875-fc3afe9252bb.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Promote deployment by creating domain name.
</p>
<br />

<p>
<img src="https://user-images.githubusercontent.com/131008349/233232929-20655c30-143f-451c-82d9-f30d0954a11c.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create password for domain. 
</p>
<br />

<p>
<img src="https://user-images.githubusercontent.com/131008349/233233217-f81987c0-029e-49ae-8c56-029b3b81aa03.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Right click the domain in the left side action menu and add organizational units - one for "_Employees" and another for "_Admins".
</p>
<br />

<p>
<img src="https://user-images.githubusercontent.com/131008349/233233944-105f7b01-e539-42af-8901-0d2a07d5b90a.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In the "_Admins" organizational unit, create an admin user.
</p>
<br />

<p>
<img src="https://user-images.githubusercontent.com/131008349/233234588-ceab6b33-cc86-4d74-91ca-b88ecffb1c77.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Make new user an admin by going to the properties and assigning the user to be apart of the "Domain Admins".
</p>
<br />

<p>
<img src="https://user-images.githubusercontent.com/131008349/233234983-d2b3cc39-fcc7-4fc6-a64f-b0e98d8afa0b.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Login the Domain Controller with the admin credentials. You might have to use the domain name.com\admin logon name.
</p>
<br />

<p>
<img src="https://user-images.githubusercontent.com/131008349/233235296-2f5234c3-de70-480a-83aa-8123b9be6dce.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Then login to the client VM using the admin login credentials. Again, you might have to use the domain name.com\admin logon name to gain access. 
</p>
<br />

<p>
<img src="https://user-images.githubusercontent.com/131008349/233235614-a400e791-eeda-41c1-9062-ef2f2d768275.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Right click the start menu and click "Settings", "Systems", then "Remote Desktop" on the left side action menu. In the advanced settings, allow the domain users group to remote into the client VM. 
</p>
<br />

<p>
<img src="https://user-images.githubusercontent.com/131008349/233235908-9033f503-1d32-4588-bca4-3d026bb90844.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In Azure, locate the client vm, in the left side action menu click "Networking", then "Network interface" and make the client VM DNS settings the Domain Controller's private IP address.
</p>
<br />

<p>
<img src="https://user-images.githubusercontent.com/131008349/233236296-a9bccff8-0acb-437c-8c5c-6ccd1fcd557f.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://user-images.githubusercontent.com/131008349/233236675-0d811da3-81ad-44f3-aae8-7813b3fbabad.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://user-images.githubusercontent.com/131008349/233237042-21ca6256-3c48-401a-a3cf-fee81db8231c.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://user-images.githubusercontent.com/131008349/233237680-4630bbf1-6a64-431f-a2a0-45c8050eca7a.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
