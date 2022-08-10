---
description: 10.10.10.11
---

# Arctic

## Nmap

```
sudo nmap -Pn -p- 10.10.10.11 --min-rate=5000
```

![](<../../../../.gitbook/assets/image (8).png>)

Ran a script script based on open ports

{% code overflow="wrap" %}
```bash
# Nmap 7.92 scan initiated Wed Aug 10 16:56:59 2022 as: nmap -Pn -p135,8500,49154 -sCV -O -v -oN script-scan.txt 10.10.10.11
Nmap scan report for arctic.htb (10.10.10.11)
Host is up (0.040s latency).

PORT      STATE SERVICE VERSION
135/tcp   open  msrpc   Microsoft Windows RPC
8500/tcp  open  fmtp?
49154/tcp open  msrpc   Microsoft Windows RPC
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose|phone|specialized
Running (JUST GUESSING): Microsoft Windows 8|Phone|2008|7|8.1|Vista|2012 (92%)
OS CPE: cpe:/o:microsoft:windows_8 cpe:/o:microsoft:windows cpe:/o:microsoft:windows_server_2008:r2 cpe:/o:microsoft:windows_7 cpe:/o:microsoft:windows_8.1 cpe:/o:microsoft:windows_vista::- cpe:/o:microsoft:windows_vista::sp1 cpe:/o:microsoft:windows_server_2012
Aggressive OS guesses: Microsoft Windows 8.1 Update 1 (92%), Microsoft Windows Phone 7.5 or 8.0 (92%), Microsoft Windows 7 or Windows Server 2008 R2 (91%), Microsoft Windows Server 2008 R2 (91%), Microsoft Windows Server 2008 R2 or Windows 8.1 (91%), Microsoft Windows Server 2008 R2 SP1 or Windows 8 (91%), Microsoft Windows 7 (91%), Microsoft Windows 7 Professional or Windows 8 (91%), Microsoft Windows 7 SP1 or Windows Server 2008 R2 (91%), Microsoft Windows 7 SP1 or Windows Server 2008 SP2 or 2008 R2 SP1 (91%)
No exact OS matches for host (test conditions non-ideal).
Uptime guess: 0.009 days (since Wed Aug 10 16:46:55 2022)
TCP Sequence Prediction: Difficulty=261 (Good luck!)
IP ID Sequence Generation: Incremental
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Read data files from: /usr/bin/../share/nmap
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Wed Aug 10 16:59:18 2022 -- 1 IP address (1 host up) scanned in 139.14 seconds
```
{% endcode %}

## FMTP Port 8500

{% embed url="https://www.eurocontrol.int/service/flight-message-transfer-protocol-address-coordination" %}

> Flight Message Transfer Protocol (FMTP) is a communication stack based on the transmission control and internet protocols (TCP/IP). It is used in a peer-to-peer communication context for the information exchange between flight data processing systems for the purpose of notification, coordination and transfer of flights between air traffic control units and for the purposes of civil-military cooperation.

I look to see if there's anything interesting that can be looked at on the browser on this particular port

![](<../../../../.gitbook/assets/image (5).png>)

Clicking on `CFIDE` leads to some pretty interesting findings

![](<../../../../.gitbook/assets/image (11).png>)

I'm most interested in the `administrator` link, so going there takes me to an Admin page!

![](<../../../../.gitbook/assets/image (7).png>)

## Searchsploit

I search for any public exploits in searchsploit

![](<../../../../.gitbook/assets/image (9).png>)

The Remote Code Execution python script catches my eye so I'll view that one

![](<../../../../.gitbook/assets/image (6).png>)

{% embed url="https://www.exploit-db.com/exploits/50057" %}

{% embed url="https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2009-2265" %}

> Multiple directory traversal vulnerabilities in FCKeditor before 2.6.4.1 allow remote attackers to create executable files in arbitrary directories via directory traversal sequences in the input to unspecified connector modules, as exploited in the wild for remote code execution in July 2009, related to the file browser and the editor/filemanager/connectors/ directory.

## Foothold #1 - RCE Script

This python script does it all! We'll change the listening host IP and port number (in case firewall rules don't like weird port numbers)&#x20;

Then we run it and get a shell!

![](<../../../../.gitbook/assets/image (2).png>)

## Foothold #2 - Directory Traversal

There was also a metasploit module for directory traversal. I was curious about it so I checked it out and found this

{% embed url="https://www.exploit-db.com/exploits/14641" %}

![](<../../../../.gitbook/assets/image (4).png>)

I decided to do this without the python script since you technically don't need to

{% code overflow="wrap" %}
```
http://arctic.htb:8500/CFIDE/administrator/enter.cfm?locale=../../../../../../../../../../ColdFusion8/lib/password.properties%00en
```
{% endcode %}

As you can see, there's a password that's encrypted, so we should crack it.

### Cracking the hash

![](../../../../.gitbook/assets/image.png)

```
happyday
```



From my understanding, essentially whatever password you type, it takes the encrypted form of it and checks if it matches the valid one. Which is why when you type a password, or just hit login, you get this weird string of weird numbers and letters

![](<../../../../.gitbook/assets/image (1).png>)

Here I'm typing in `password`

![](<../../../../.gitbook/assets/image (74).png>)

![](<../../../../.gitbook/assets/image (76).png>)

It's the same length, however it didn't get cracked. However I believe, theoretically, this is how it works.

![](<../../../../.gitbook/assets/image (75).png>)



## Priv Esc
