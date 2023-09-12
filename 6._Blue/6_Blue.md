# 6. Blue

  
nmap -sV 10.10.249.97  
  
Starting Nmap 7.80 ( <https://nmap.org> ) at 2020-03-23 20:15 EDT  
Nmap scan report for 10.10.249.97  
Host is up (0.14s latency).  
Not shown: 991 closed ports  
PORT STATE SERVICE VERSION  
135/tcp open msrpc Microsoft Windows RPC  
139/tcp open netbios-ssn Microsoft Windows netbios-ssn  
445/tcp open microsoft-ds Microsoft Windows 7 - 10 microsoft-ds (workgroup: WORKGROUP)  
3389/tcp open ssl/ms-wbt-server?  
49152/tcp open msrpc Microsoft Windows RPC   
49153/tcp open msrpc Microsoft Windows RPC   
49154/tcp open msrpc Microsoft Windows RPC  
49158/tcp open msrpc Microsoft Windows RPC  
49160/tcp open msrpc Microsoft Windows RPC  
Service Info: Host: JON-PC; OS: Windows; CPE: cpe:/o:microsoft:windows  
  
Service detection performed. Please report any incorrect results at <https://nmap.org/submit/> .  
Nmap done: 1 IP address (1 host up) scanned in 76.52 seconds  
