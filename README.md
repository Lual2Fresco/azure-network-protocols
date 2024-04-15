<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we explore network traffic to and from Azure Virtual Machines using Wireshark and experiment with Network Security Groups. 

This is a continuation, utilizing the same Virtual Machines and some of the same environments from the previous repository, to demonstrate Active Directory functionality. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04


<h2>Actions and Observations</h2>

<p>
To start, access the Domain Controller using an Admin account and launch Active Directory Users and Computers. Then, log in to the Windows 10 VM using any user account within the Domain.

</p>
<br />

<p>
<img src="https://i.imgur.com/GDF0i7Q.png." height="80%" width="80%" alt="Disk Sanitization Steps"/> <img src="https://i.imgur.com/3gq5GXY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <img src="https://i.imgur.com/iY4YD46.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
On the Domain Controller's C:\ drive, create four folders: "read-access," "write-access," "no-access," and "accounting." These names are for this example. Share the "read" and "write" folders with the "Domain Users" group, assigning read-only and read/write permissions respectively. Share only the "no-access" folder with the "Domain Users" group assigning read/write permissions.
</p>
<br />

<p>
<img src="https://i.imgur.com/zjKGcjQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <img src="https://i.imgur.com/WPFpBdG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <img src="https://i.imgur.com/IQ6RHbb.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <img src="https://i.imgur.com/sWuRWWC.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Moving forward, return to the user on the Windows 10 VM and launch File Explorer. In the search bar, type \dc-1. This action will display the files shared on the Domain Network.
</p>
<br />

<p>
<img src="https://i.imgur.com/in0XT6Y.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <img src="https://i.imgur.com/YUyAChq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Observe that as a user, access to the "no-access" folder is restricted. Additionally, the "accounting" folder remains inaccessible, as no actions have been taken on it yet.
</p>
<br />

<p>
<img src="https://i.imgur.com/yd035UU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <img src="https://i.imgur.com/Fs3n3zL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>
Note that while we can access the "read-access" folder, we are unable to create any content within it. Conversely, we have the ability to create documents within the "write-access" folder.
</p>
<br />

<p>
<img src="https://i.imgur.com/xC0v21c.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <img src="https://i.imgur.com/cD74wri.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <img src="https://i.imgur.com/UcGt3oy.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>
Next, in Active Directory Users & Computers, generate a New Organizational Unit labeled "_SECURITY GROUPS." Within this new Organizational Unit, establish a group titled "ACCOUNTANTS."
</p>
<br />

<p>
<img src="https://i.imgur.com/WM1VRet.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <img src="https://i.imgur.com/UxYwEOp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <img src="https://i.imgur.com/P3WrYgV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
Afterward, navigate back to the accounting folder and share it with the "ACCOUNTANTS" group, granting them read/write permissions. Confirm that the current user on Client-1 still does not have access to the accounting group.
</p>
<br />

<p>
<img src="https://i.imgur.com/XIi084D.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <img src="https://i.imgur.com/7nrAS8N.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> 
</p>
In this step, we're accessing the properties of the ACCOUNTANTS group on the Domain controller. We're navigating to the members tab to add any domain user to the group.
</p>
<br />

<p>
<img src="https://i.imgur.com/VXpyWBV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <img src="https://i.imgur.com/zldeJxl.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> 
</p>
If the change to folder accessibility was made while the user was still logged in, the folder will remain inaccessible until the user logs out and logs back in for the change to take effect. Now, as a member of the ACCOUNTANTS group, the user has access to the folder.
</p>
<br />

<p>
<img src="https://i.imgur.com/h5F5F4P.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> 
</p>
