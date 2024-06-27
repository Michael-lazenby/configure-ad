<p align="center">
<img src="https://i.imgur.com/w7amRI0.png" height="40%" width="60%"/>
</p>

<h1>Configuring On-premises Active Directory within Azure VMs</h1>In this project, I configured on-premises Active Directory and created user accounts with PowerShell within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>Key Objectives</h2>

<h2>Active Directory Installation</h2>
<p>Configure and install Active Directory services on the designated Domain Controller virtual machine.<p>


<h2>Summary</h2>

<p>
I created two virtual machines in Azure, one with Windows Server 2022 and the other with Windows 10. The Windows 2022 virtual machine would be the domain controller, and the Windows 10 virtual machine would be the client machine. I had to switch the Domain controller's NIC private IP address from Dynamic to Static. The reason I did this was that when I configured the client's DNS settings, the Domain controller's IP address would still be the same. I also viewed the topology in Azure Network Watcher to make sure both devices were on the network and subnet.
</p>
<img src="https://i.imgur.com/ti0b95l.png" height="70%" width="70%"/>
<br />

<h3>Connecting with RDP and firewall modifications</h3>
<p>
I connected both devices using Remote Desktop, and then I initiated a continuous ping from the Client to the Domain controller to ensure connectivity. The requests were timing out, so I changed the setting in Windows Defender Firewall in the DC and enabled Networking Diagnostics (ICMPv4 protocol). This allowed the Domain Controller to reply to the requests.</p>
<p>
<img src="https://i.imgur.com/YvrBTgj.png" height="70%" width="70%"/>
</p>
<p>
<img src="https://i.imgur.com/ym3Ld63.png" height="70%" width="70%"/>
</p>
<p>
<img src="https://i.imgur.com/LccuYWf.png" height="70%" width="70%"/>
</p>
<br />

<h3>Installing Active Directory</h3>
<p>
I installed Active Directory Domain Services (AD DS) from the Server Manager Dashboard. Once AD DS was installed, I promoted the machine to a Domain Controller so that it could manage devices and accounts on the domain.
</p>
<p>
<img src="https://i.imgur.com/AayPHkb.png" height="70%" width="70%"/>
</p>
<p>
<img src="https://i.imgur.com/XqzeZYs.png" height="70%" width="70%"/>
</p>
<br />

<p>
<img src="https://i.imgur.com/jbCeryh.png" height="70%" width="70%"/>
</p>
<p>
Now that Active Directory was all set up, I added two organizational units (OU) and a user. The OUs were _ADMINS and _EMPLOYEES, and the new user was “Jane Doe.” Jane was going to be an administrator, so I created her account inside the _ADMINS OU and added her as a member of Domain Admins. I logged out of the default account that I started with and logged back in as Jane.
</p>
<br />


<p>
I went back to Azure and set the DC’s private IP address as the DNS server for the Client. After this, I was able to join the Client in my domain. This was confirmed by the “Welcome” box that popped up, confirming that the Client was now part of the domain.
</p>
<img src="https://i.imgur.com/afGXoqY.png" height="70%" width="70%"/>
</p>
<p>
<img src="https://i.imgur.com/31ZSBHk.png" height="70%" width="70%"/>
</p>
<br />


<h3>Enabling Remote Desktop for users</h3>
<p>
I enabled Domain Users to use Remote Desktop to access the Client. Remote Desktop is the only way to log into the virtual machine, so enabling this for Domain Users would allow any user accounts in the domain to be able to log into this machine.
</p>
<img src="https://i.imgur.com/EWzPnOh.png" height="70%" width="70%"/>
<br />


<h3>Powershell Script</h3>
<p>
I created 10,000 user accounts using a PowerShell script. All of the accounts were placed into the _EMPLOYEES OU, so I selected a random account and used it to log into the Client. I used the commands “hostname” and “whoami” in the command-line, which confirmed that this was successful.
</p>
<img src="https://i.imgur.com/lzUMtp1.png" height="70%" width="70%"/>
<img src="https://i.imgur.com/WF5lwhY.png" height="70%" width="70%"/>
<br />

