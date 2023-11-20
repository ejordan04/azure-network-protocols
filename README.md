<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create Resource
- Observe ICMP Traffic
- Observe SSH Traffic
- Observe DHCP Traffic
- Observe DNS Traffic
- Observe RDP Traffic

<h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
First, create a resource group in Microsoft Azure. We'll be using two Virtual Machines (VMs) one running Windows 10 and another running Linux (Ubuntu). Make sure they are in the same Virtual Network (Vnet).
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Use Remote Desktop to connect to the Windows 10 VM. Once connected, install Wireshark. After Wireshark is installed, open it and filter for ICMP traffic only. Locate the private IP address of the Ubuntu VM within Azure and then ping it from within the Windows 10 VM using either the command line or PowerShell. Observe the ping requests and replies. Now, initiate a perpetual ping from our Windows 10 VM to the Ubuntu VM. Next, we'll open the Network Security Group that our Ubuntu VM is using and disable incoming (inbound) ICMP traffic. After observing the differences in Wireshark, re-enable ICMP traffic.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now back in Wireshark, filter for SSH traffic only. From our Windows 10 VM, we're going to SSH into our Ubuntu VM using its private IP address. To do this, we use the command ssh username@ip.address. After entering the password, we should have access to the Ubuntu VM, and you can tell because our username changed colors. To leave, type exit.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Going back inside Wireshark, filter for DHCP traffic only, and from our Windows 10 VM attempt to issue it a new IP address using the command ipconfig /renew. 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now filter for DNS traffic only. From our Windows 10 VM, we're going to use nslookup to see what google.com's IP address is. 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lastly, filter for RDP traffic or specifically tcp.port==3389. We will see non-stop spam traffic because the RDP protocol is constantly showing us a live stream from one computer to another therefor traffic is always being transmitted.
</p>
<br />
