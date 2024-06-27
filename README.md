<p align="center">
<img src="https://i.imgur.com/w7amRI0.png" height="40%" width="60%"/>
</p>

<h1>Configuring On-premises Active Directory within Azure VMs</h1>In this project, I configured on-premises Active Directory and created user accounts with PowerShell within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h3>Operating Systems Used </h3>

- Windows Server 2022
- Windows 10 (21H2)

<h3>Key Objectives</h3>

<h3>Active Directory Installation</h3>
<p>Configure and install Active Directory services on the designated Domain Controller virtual machine<p>

<h3>Forest Creation</h3>
<p>Establish a new Active Directory forest</p>

<h3>Administrator Account Creation</h3>
<p>Create and administer user accounts with administrative privileges for effective management of the Active Directory environment</p>

<h3>Domain Joining</h3>
<p>Integrate the virtual machine into the existing domain to ensure seamless communication with the Active Directory infrastructure</p>

<h3>Remote Desktop Setup</h3>
<p>Configure Remote Desktop access specifically tailored for non-administrative users, enhancing user accessibility while maintaining security protocols</p>

<h2>Configuration</h2>

<h3> Install Active Directory in DC</h3>
<p>
In the Server Manager dashboard, click on "Add roles and features" and follow the setup instructions.
<p>


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

