# Azure-Inspecting-Network-Traffic-using-Wireshark

<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h2> Intro </h2>

- Creating Resource groups
- Creating Azure Virtual Networks and Subnets
- Using Azure VMs Windows and Ubuntu Linux
- Using Azure Network Security Groups 
- Configuring a firewall to allow/deny specific traffic
- Wireshark Installation
- Use of command line tools

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop Connection
- Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 Pro (22H2)
- Ubuntu Server 20.04



<h2>Step by Step Guide</h2>

To begin we will install wireshark by going to our internet browser of choice and look up wireshark, we will navigate to www.wireshark.org > Get Started > Windows x64 Installer.
We will run the installer, and install with default configurations, hitting next until we are complete.


<p>
<img src="https://i.imgur.com/aRimquU.png" height="80%" width="80%" alt="Azure Networking Steps"/>
</p>
<p>

</p>
<br />

<p>
<img src="https://i.imgur.com/CXLdX1F.png" height="80%" width="80%" alt="Azure Networking Steps"/>
</p>
<p>
We can start capturing packets with the first button in our toolbar and we will be immediately spammed with network traffic

</p>
<br />

<p>
<img src="https://i.imgur.com/IUYhBnr.png" height="80%" width="80%" alt="Azure Networking Steps"/>
</p>
<p>

</p>
<br />

<p>
<img src="https://i.imgur.com/O0lXAmd.png" height="80%" width="80%" alt="Azure Networking Steps"/>
</p>
<p>
To fix this we can filter specific traffic by typing in the display filter bar and type in "icmp"

</p>
<br />

<p>
<img src="https://i.imgur.com/fDtuLo9.png" height="80%" width="80%" alt="Azure Networking Steps"/>
</p>
<p>
Now we will get VM2’s private IP of our from Azure portal

</p>
<br />

<p>
<img src="https://i.imgur.com/2JF0e6L.png" height="80%" width="80%" alt="Azure Networking Steps"/>
</p>
<p>
We will use this to test the private network connectivity on VM1 by opening up a Windows command line for example PowerShell. Then go on and ping the private IP. We will then see our icmp traffic come up on Wireshark

</p>
<br />

<p>
<img src="https://i.imgur.com/EbLV6bv.png" height="80%" width="80%" alt="Azure Networking Steps"/>
</p>

<p>
<img src="https://i.imgur.com/FfQX09l.png" height="80%" width="80%" alt="Azure Networking Steps"/>
</p>
<br />
We can then run the same test on www.google.com and force it to use the IPv4 address using this command at the end of our ping command. “ping www.google.com -4” Here are the results

<p>
<img src="https://i.imgur.com/tNeMHDT.png" height="80%" width="80%" alt="Azure Networking Steps"/>
</p>
<p>
x
</p>
<br />

Another command we can use is “-t” to do a continuous transmission on our ping command.

<p>
<img src="https://i.imgur.com/N5Z3Nle.png" height="80%" width="80%" alt="Azure Networking Steps"/>
</p>

We can then navigate out of our VM’s and within the Azure portal search for Network Security Groups and attempt to block icmp traffic by changing the inbound rules.
Network Security Groups > VM2-nsg > Settings > Inbound security rules > Add, and configure the rule to these specific settings

<p>
<img src="https://i.imgur.com/uxW4og8.png" height="80%" width="80%" alt="Azure Networking Steps"/>
</p>

<p>
<img src="https://i.imgur.com/2KbfFTE.png" height="80%" width="80%" alt="Azure Networking Steps"/>
</p>
We should be able to see the change take effect here within a few moments. Instead of seeing request reply, request reply, etc. on Wireshark then we can tell the Network Security Group firewall has taken effect.

<p>
<img src="https://i.imgur.com/hY9YJSJ.png" height="80%" width="80%" alt="Azure Networking Steps"/>
</p>
Instead of deleting and adding a new inbound rule, we can edit our rule and set icmp traffic to allow. This should change the request, request, request… back to request, reply, request, reply…

<p>
<img src="https://i.imgur.com/0iwkL6y.png" height="80%" width="80%" alt="Azure Networking Steps"/>
</p>

<p>
<img src="https://i.imgur.com/eTvGzxQ.png" height="80%" width="80%" alt="Azure Networking Steps"/>
</p>
We will now change our filter from “icmp” to “ssh” OR “tcp.port == 22” and enter the command into our command line “ssh labuser@10.0.0.6” aka “ssh [USER]@[VM2 PRIVATE IP]” > yes > enter password. We can see our SSH traffic being displayed within Wireshark.

<p>
<img src="https://i.imgur.com/ioVjTKD.png" height="80%" width="80%" alt="Azure Networking Steps"/>
</p>
Now we need to logout of the Linux command line and go back to Windows using the command “exit”. Next we can also try viewing DHCP traffic so we will change the filter to “dhcp” and enter the command “ipconfig /renew”. This should be the result.
<p>
<img src="https://i.imgur.com/CZNMjgX.png" height="80%" width="80%" alt="Azure Networking Steps"/>
</p>
Now we will change the filter to dns, and use the command “nslookup www.google.com” to retrieve and view DNS traffic with Wireshark

<p>
<img src="https://i.imgur.com/xuD7zCV.png" height="80%" width="80%" alt="Azure Networking Steps"/>
</p>

We can also view our RDP traffic by changing the filter to “tcp.port ==3389” which is being displayed since we are connected to the VM using Remote Desktop Connection.

<p>
<img src="https://i.imgur.com/qPB6q1e.png" height="80%" width="80%" alt="Azure Networking Steps"/>
</p>

<h2>Lessons Learned </h2>
With this lab I was able to build intuition for Wireshark, a widely recognized and used program that is used to monitor packets. I can now understand how to install wireshark, ping within a private network, and block network traffic using a network security group firewall. Observed traffic starting and stopping based on firewall rules. Observed SSH between the 2 VMs. Observed using ICMP, SMTP, DNS, RDP, and DHCP traffic. I learned some little things too like if you filter using caps it will not work, the input must be in lowercase. I also learned how simple it is to set up firewall rules and configure them within Azure.
