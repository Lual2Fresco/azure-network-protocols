<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we explore network traffic to and from Azure Virtual Machines using Wireshark and experiment with Network Security Groups. 
<br />


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
Create a Resource Group in Microsoft Azure and set up two Virtual Machines within it—one running Windows 10 and the other Ubuntu. Ensure both Virtual Machines are on the same Virtual Network.

</p>
<br />

<p>
<img src="https://i.imgur.com/uVEiNmE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <img src="https://i.imgur.com/vrCmK08.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <img src="https://i.imgur.com/0uHKYrW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Access the Windows VM using Remote Desktop and download Wireshark to monitor network traffic within the VM.
</p>
<br />

<p>
<img src="https://i.imgur.com/H0fzCdU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <img src="https://i.imgur.com/DKuJmg6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> 
</p>
<p>
When you start capturing packets, Wireshark will display all the traffic and protocols running in the background.
</p>
<br />

<p>
<img src="https://i.imgur.com/p1l9A7W.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> 
</p>
<p>
Apply an ICMP filter to observe the traffic between our two virtual machines. By pinging the private IP address of the other VM, we can observe the ICMP protocol using the private IP of the VM initiating the ping, along with the ping request and reply.
</p>
<br />

<p>
<img src="https://i.imgur.com/H6w2Sy5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <img src="https://i.imgur.com/rDVmFey.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>
In this instance, I pinged Google instead of the other VM. We can observe the response from Google's IP address.
</p>
<br />

<p>
<img src="https://i.imgur.com/RXU2oy0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> 
<p>
Here, I initiate a continuous ping to the second VM to observe how firewalls operate.
</p>
<br />

<p>
<img src="https://i.imgur.com/0D6Mb5M.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> 
</p>
ICMP is the protocol used when you ping the VM. To block this traffic, I return to Azure, access the Ubuntu VM, and set a rule to block all ICMP traffic.
</p>
<br />

<p>
<img src="https://i.imgur.com/CCXFKKE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <img src="https://i.imgur.com/EPfuV5K.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> 
</p>
Deleting or modifying the rule to allow ICMP traffic will enable the request and replies to continue flowing through.
</p>
<br />

<p>
<img src="https://i.imgur.com/XR1Uovj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <img src="https://i.imgur.com/pOfxqWl.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> 
</p>
Here, we can observe SSH traffic. 
</p>
<br />

<p>
<img src="https://i.imgur.com/sIXKVaa.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <img src="https://i.imgur.com/foP3T9p.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> 
</p>
<br />

This allows access to the Command Line of the other VM, with traffic being visible for every text or command entered.
</p>
<br />

<p>
<img src="https://i.imgur.com/6YdILQY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> 
</p>
<br />

Here, DHCP traffic was observed. Upon using the command "ipconfig /renew," DHCP reissued our IP address.
</p>
<br />

<p>
<img src="https://i.imgur.com/ImiNu7c.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <img src="https://i.imgur.com/h5F5F4P.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> 
</p>
<br />

Here, we observe DNS traffic. By using the command "nslookup," we can notice the different IP addresses as well as other information associated with these websites.
</p>
<br />

<p>
<img src="https://i.imgur.com/MO9423w.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> 
