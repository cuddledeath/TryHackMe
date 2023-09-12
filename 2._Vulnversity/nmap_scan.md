# nmap scan

  
Starting Nmap 7.80 ( https://nmap.org ) at 2020-03-12 18:01 EDT  
Nmap scan report for 10.10.186.245  
Host is up (0.12s latency).  
Not shown: 994 closed ports  
PORT STATE SERVICE VERSION  
21/tcp open ftp vsftpd 3.0.3  
22/tcp open ssh OpenSSH 7.2p2 Ubuntu 4ubuntu2.7 (Ubuntu Linux; protocol 2.0)  
| ssh-hostkey:   
| 2048 5a:4f:fc:b8:c8:76:1c:b5:85:1c:ac:b2:86:41:1c:5a (RSA)  
| 256 ac:9d:ec:44:61:0c:28:85:00:88:e9:68:e9:d0:cb:3d (ECDSA)  
|\_ 256 30:50:cb:70:5a:86:57:22:cb:52:d9:36:34:dc:a5:58 (ED25519)  
139/tcp open netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)  
445/tcp open netbios-ssn Samba smbd 4.3.11-Ubuntu (workgroup: WORKGROUP)  
3128/tcp open http-proxy Squid http proxy 3.5.12  
|\_http-server-header: squid/3.5.12  
|\_http-title: ERROR: The requested URL could not be retrieved  
3333/tcp open http Apache httpd 2.4.18 ((Ubuntu))  
|\_http-server-header: Apache/2.4.18 (Ubuntu)  
|\_http-title: Vuln University  
Service Info: Host: VULNUNIVERSITY; OSs: Unix, Linux; CPE: cpe:/o:linux:linux\_kernel  
  
Host script results:  
|\_clock-skew: mean: 1h20m00s, deviation: 2h18m33s, median: 0s  
|\_nbstat: NetBIOS name: VULNUNIVERSITY, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)  
| smb-os-discovery:   
| OS: Windows 6.1 (Samba 4.3.11-Ubuntu)  
| Computer name: vulnuniversity  
| NetBIOS computer name: VULNUNIVERSITY\x00  
| Domain name: \x00  
| FQDN: vulnuniversity  
|\_ System time: 2020-03-12T18:02:28-04:00  
| smb-security-mode:   
| account\_used: guest  
| authentication\_level: user  
| challenge\_response: supported  
|\_ message\_signing: disabled (dangerous, but default)  
| smb2-security-mode:   
| 2.02:   
|\_ Message signing enabled but not required  
| smb2-time:   
| date: 2020-03-12T22:02:29  
|\_ start\_date: N/A