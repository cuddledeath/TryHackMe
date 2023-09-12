# nmap

  
Starting Nmap 7.80 ( <https://nmap.org> ) at 2020-03-14 20:08 EDT  
Nmap scan report for 10.10.99.189  
Host is up (0.13s latency).  
Not shown: 998 closed ports  
PORT STATE SERVICE VERSION  
22/tcp open ssh OpenSSH 7.2p2 Ubuntu 4ubuntu2.6 (Ubuntu Linux; protocol 2.0)  
| ssh-hostkey:   
| 2048 e9:63:a6:37:62:75:27:9c:d8:66:ca:ab:eb:b0:3d:80 (RSA)  
| 256 a9:59:09:13:bd:1c:05:e7:8d:89:01:db:4b:6b:5d:c0 (ECDSA)  
|\_ 256 ba:43:46:10:8c:13:b3:25:f8:09:58:26:e3:97:6c:1d (ED25519)  
80/tcp open http Node.js Express framework  
|\_http-cors: HEAD GET POST PUT DELETE PATCH  
| http-robots.txt: 1 disallowed entry   
|\_/ftp  
|\_http-title: OWASP Juice Shop  
Service Info: OS: Linux; CPE: cpe:/o:linux:linux\_kernel  
  
Service detection performed. Please report any incorrect results at <https://nmap.org/submit/> .  
Nmap done: 1 IP address (1 host up) scanned in 33.06 seconds