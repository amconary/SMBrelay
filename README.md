<h1>SMB Relay Attack</h1>

 <h2>Description</h2>
Project consists of performing a SMB relay attack, a type of technique using a malicious relay server to obtain password hashes from SMB, on a vulnerable Windows home lab.
<br />


<h2>Languages and Utilities Used</h2>

- <b>Responder</b> 
- <b>Nmap</b>
- <b>Mousepad</b>
- <b>Netcat</b>
- <b>Impacket-ntlmrelayx</b>

<h2>Environments Used </h2>

- <b>Kali Linux</b>

<h2>Project walk-through:</h2>

<p align="center">
SMB Relay Attack 
<br />
<br />
First lets test our target to see if SMB signing is enabled on the host. Open a terminal and run nmap scan using a script to check against port 445. <br />
<img src="https://i.imgur.com/F5sxQek.png" height="80%" width="80%" alt="SMBattack"/>
<br />
<br />
We can see here that SMB signing is not required on this machine. Next we need to edit the Responder config file to turn the SMB and HTTP options to off. This we allow us to perform a relay attack.  <br/>
<img src="https://i.imgur.com/SAq69VA.png" height="60%" width="60%" alt="SMBattack"/>
<br />
<br />
Run Responder with the modified config.  <br/>
<img src="https://i.imgur.com/pK8n1iT.png" height="60%" width="60%" alt="SMBattack"/>
<br />
<br />
Next we will run impacket-ntlmrelayx, this tool will relay any hashes over to this server then over to our target listed in the targets.txt file.  <br/>
<img src="https://i.imgur.com/6yIts3V.png" height="60%" width="60%" alt="SMBattack"/>
<br />
<br />
Now to force a connection for testing we will attempt to browser to our attacker machine on our win 10 VM which will establish a connection, and since we have administrator access on another PC on the network it will then dump all the local hashes for us.  <br/>
<img src="https://i.imgur.com/BhvdYPO.png" height="60%" width="60%" alt="SMBattack"/>
<br />
<br />
We can now crack or use these hashes to perform additional attacks.
<br />
<br />
</p>
<p align="left">
Mitigation/Remediation Strategies <br />
1. Enable SMB signing on all devices - blocks the attack completely <br />
2. Disable NTLM authentication on network - blocks the attack <br />
3. Monitor and limit admin accounts - reduce the attack surface <br />
<br />
<br />
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
