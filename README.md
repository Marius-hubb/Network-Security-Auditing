<h1>Network Troubleshooting using Command Line Utilities and Tools</h1>

 ## [Video Demonstration (38:41)](https://drive.google.com/file/d/1ozfcxE80ODhxWV1-2v5EPMv1_uyHX-eD/view?usp=drive_link)

<h2>Description</h2>

This lab will demonstrate how to perform network troubleshooting using command-line utilities and tools.

## Lab Walk Through
#### nslookup 
nalookup is a command-line tool used to query DNS servers to obtain domain name or IP address information.
- **`nslookup`** to enter nslookup interactive mode.
- **`set type=a`** to configure nslookup to query for the IP address of a given domain.
- Type the target domain **`www.certifiedhacker.com`** to obtain the IP address, as shown in the screenshot below:

<p align="center"> <img src="https://i.imgur.com/J9Ntu90.png" height="50%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<p align="left">The first two lines in the result are as follows:<br/>
 Server: pfSense.localdomain and Address: 10.10.1.1<br/>
<br/>
This specifies that the result was directed to the default server hosted on the local network (pfSense Firewall) that resolves the requested domain.<br/>
<br/>
Thus, if the response is coming from your local machine’s server (pfSense), but not the server that legitimately hosts the domain www.certifiedhacker.com; it is considered to be a non-authoritative answer. Here, the IP address of the target domain www.certifiedhacker.com is 162.241.216.11. Since the result returned is non-authoritative I need to obtain the domain's authoritative name server. <br/>

- **`set type=cname`** to lookup the CNAME directly against the domain's authoritative name server
- **`certifiedhacker.com`** to specify the domain<br/>
This returns the domain’s authoritative name server (ns1.bluehost.com), along with the mail server address (dnsadmin.box5331.bluehost.com), as shown in the screenshot below.<br/>

<p align="center"><img src="https://i.imgur.com/LoH6AcF.png" height="50%" width="80%" alt="Disk Sanitization Steps"/>
<br />

 - Since I have obtained the authoritative name server ns1.bluehost.com I can run **`set type=a`** to get the IP address of the server. The IP address is displayed below as 162.159.24.80:
<p align="center"> 
<img src="https://i.imgur.com/isf8qig.png" height="50%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<p align="left"> The authoritative name server stores the records associated with the domain. Therefore, if an attacker can determine the authoritative name server (primary name server) and obtain its associated IP address, he/she might attempt to exploit the server to perform attacks such as DoS, DDoS, URL Redirection, etc.

#### tracert 
tracert can be used to view the hops that the packets made before reaching the destination.
- **`tracert certifiedhacker.com`** 
 <p align="center">
<img src="https://i.imgur.com/7QhMwE8.png" height="50%" width="80%" alt="Disk Sanitization Steps"/>
<br />

#### arp -a
- **`arp -a`** shows a list of IP addresses and their corresponding MAC addresses that the computer has recently communicated with.
<p align="center">
<img src="https://i.imgur.com/JbKAnHd.png" height="50%" width="80%" alt="Disk Sanitization Steps"/>
<br />

#### pathping
- pathping utility provides detailed information about the path characteristics from a specific host to a specific destination in a single picture by combining the ping and tracert/traceroute commands.
- **`pathping -n www.certifiedhacker.com`**
<p align="center">
<img src="https://i.imgur.com/IjpO2Km.png" height="50%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

<p align="center">
<br/>
<img src="https://i.imgur.com/rHWY0PS.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
<br />
<br />
<p align="center">
<br/>
<img src="https://i.imgur.com/4vy91SK.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
<br />
<br />

