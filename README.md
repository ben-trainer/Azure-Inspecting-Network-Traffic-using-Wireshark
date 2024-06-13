# Azure-Inspecting-Network-Traffic-using-Wireshark

<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Inspecting Traffic Between Azure Virtual Machines</h1>
x <br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop Connection
- Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 Pro (22H2)
- Ubuntu Server 20.04

<h2>The Set-Up</h2>

x 

<h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/DutP0XT.png" height="80%" width="80%" alt="Azure Networking Steps"/>
</p>
<p>
Using Remote Desktop Connection, I connect to the Windows VM using its public IP address. From there, I installed Wireshark in order to begin inspecting traffic. 
</p>
<br />

<p>
<img src="https://i.imgur.com/2JQawfN.png" height="80%" width="80%" alt="Azure Networking Steps"/>
</p>
<p>
x
</p>
<br />

<p>
<img src="https://i.imgur.com/HTga2Iq.png" height="80%" width="80%" alt="Azure Networking Steps"/>
</p>
<p>
Within the Azure portal, I opened the networking settings for the Ubuntu VM and added an inbound security rule to block ICMP traffic. I make sure to have the priority higher than SSH (300) to ensure the rule applies first. 
</p>
<br />

<p>
<img src="https://i.imgur.com/i3BC2LW.png" height="80%" width="80%" alt="Azure Networking Steps"/>
</p>
<p>
Upon returning to the Windows VM, I notice that the ICMP traffic is blocked now that the inbound security rule is in place. After changing the rule to allow traffic again, the perpetual ping resolves without timing out. 
</p>
<br />

<p>
<img src="https://i.imgur.com/fDtuLo9.png" height="80%" width="80%" alt="Azure Networking Steps"/>
</p>
<p>
x
</p>
<br />

<p>
<img src="https://i.imgur.com/mptFClI.png" height="80%" width="80%" alt="Azure Networking Steps"/>
</p>
<p>
x
</p>
<br />

<p>
<img src="https://i.imgur.com/gtiupfH.png" height="80%" width="80%" alt="Azure Networking Steps"/>
</p>
<p>
x
</p>
<br />

<p>
<img src="https://i.imgur.com/N7voXYU.png" height="80%" width="80%" alt="Azure Networking Steps"/>
</p>
<p>
x
</p>
<br />

<h2>Lessons Learned </h2>
x
