# nmap

  
sudo nmap -sS 10.10.62.246  
  
Starting Nmap 7.80 ( <https://nmap.org> ) at 2020-03-24 20:51 EDT  
Nmap scan report for 10.10.62.246  
Host is up (0.14s latency).  
Not shown: 998 closed ports  
PORT STATE SERVICE  
22/tcp open ssh  
80/tcp open http  
  
Nmap done: 1 IP address (1 host up) scanned in 2.07 seconds  
  
  
sudo nmap -sS -sV -Pn 10.10.62.246  
  
Starting Nmap 7.80 ( <https://nmap.org> ) at 2020-03-24 20:52 EDT  
Stats: 0:01:21 elapsed; 0 hosts completed (1 up), 1 undergoing SYN Stealth Scan  
SYN Stealth Scan Timing: About 40.00% done; ETC: 20:56 (0:02:02 remaining)  
Nmap scan report for 10.10.62.246  
Host is up (0.13s latency).  
Not shown: 998 closed ports  
PORT STATE SERVICE VERSION  
22/tcp open ssh OpenSSH 6.6.1p1 Ubuntu 2ubuntu2.10 (Ubuntu Linux; protocol 2.0)  
80/tcp open http Apache httpd 2.4.7 ((Ubuntu))  
Service Info: OS: Linux; CPE: cpe:/o:linux:linux\_kernel  
  
Service detection performed. Please report any incorrect results at <https://nmap.org/submit/> .  
Nmap done: 1 IP address (1 host up) scanned in 92.78 seconds  
  
sudo nmap -A -Pn 10.10.62.246  
  
Starting Nmap 7.80 ( <https://nmap.org> ) at 2020-03-24 20:57 EDT  
Nmap scan report for 10.10.62.246  
Host is up (0.13s latency).  
Not shown: 998 closed ports  
PORT STATE SERVICE VERSION  
22/tcp open ssh OpenSSH 6.6.1p1 Ubuntu 2ubuntu2.10 (Ubuntu Linux; protocol 2.0)  
| ssh-hostkey:   
| 1024 73:95:58:a5:d1:56:9d:78:ae:cf:6f:0a:5e:bc:7a:56 (DSA)  
| 2048 7b:29:ba:d7:f6:2b:15:1d:0b:be:90:f2:b0:87:56:0f (RSA)  
| 256 88:91:dc:cf:d4:c1:09:be:3a:2c:8c:41:27:39:e4:6e (ECDSA)  
|\_ 256 f2:5f:c4:c8:fe:b2:d5:5c:54:52:7e:6b:d6:af:58:20 (ED25519)  
80/tcp open http Apache httpd 2.4.7 ((Ubuntu))  
| http-cookie-flags:   
| /:   
| PHPSESSID:   
|\_ httponly flag not set  
| http-robots.txt: 1 disallowed entry   
|\_/  
|\_http-server-header: Apache/2.4.7 (Ubuntu)  
| http-title: Login :: Damn Vulnerable Web Application (DVWA) v1.10 *Develop...  
|\_Requested resource was login.php  
No exact OS matches for host (If you know what OS is running on it, see <https://nmap.org/submit/> ).  
TCP/IP fingerprint:  
OS:SCAN(V=7.80%E=4%D=3/24%OT=22%CT=1%CU=37164%PV=Y%DS=2%DC=T%G=Y%TM=5E7AACC  
OS:8%P=x86\_64-pc-linux-gnu)SEQ(SP=FE%GCD=1%ISR=101%TI=Z%CI=I%II=I%TS=8)OPS(  
OS:O1=M54DST11NW7%O2=M54DST11NW7%O3=M54DNNT11NW7%O4=M54DST11NW7%O5=M54DST11  
OS:NW7%O6=M54DST11)WIN(W1=68DF%W2=68DF%W3=68DF%W4=68DF%W5=68DF%W6=68DF)ECN(  
OS:R=Y%DF=Y%T=40%W=6903%O=M54DNNSNW7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS  
OS:%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R=  
OS:Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=  
OS:R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%T  
OS:=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD=  
OS:S)  
  
Network Distance: 2 hops  
Service Info: OS: Linux; CPE: cpe:/o:linux:linux\_kernel  
  
TRACEROUTE (using port 38292/tcp)  
HOP RTT ADDRESS  
1 125.93 ms 10.8.0.1  
2 126.38 ms 10.10.62.246  
  
OS and Service detection performed. Please report any incorrect results at <https://nmap.org/submit/> .  
Nmap done: 1 IP address (1 host up) scanned in 99.59 seconds  
  
nmap --script vuln -Pn 10.10.62.246  
  
tarting Nmap 7.80 ( <https://nmap.org> ) at 2020-03-24 21:07 EDT  
Pre-scan script results:  
| broadcast-avahi-dos:   
| Discovered hosts:  
| 224.0.0.251  
| After NULL UDP avahi packet DoS (CVE-2011-1002).  
|\_ Hosts are all up (not vulnerable).  
Stats: 0:03:57 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan  
NSE Timing: About 98.52% done; ETC: 21:11 (0:00:01 remaining)  
Stats: 0:03:57 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan  
NSE Timing: About 98.52% done; ETC: 21:11 (0:00:01 remaining)  
Stats: 0:03:58 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan  
NSE Timing: About 98.52% done; ETC: 21:11 (0:00:01 remaining)  
Nmap scan report for 10.10.62.246  
Host is up (0.14s latency).  
Not shown: 998 closed ports  
PORT STATE SERVICE  
22/tcp open ssh  
|\_clamav-exec: ERROR: Script execution failed (use -d to debug)  
80/tcp open http  
|\_clamav-exec: ERROR: Script execution failed (use -d to debug)  
| http-cookie-flags:   
| /:   
| PHPSESSID:   
| httponly flag not set  
| /login.php:   
| PHPSESSID:   
|\_ httponly flag not set  
|\_http-csrf: Couldn't find any CSRF vulnerabilities.  
|\_http-dombased-xss: Couldn't find any DOM based XSS.  
| http-enum:   
| /login.php: Possible admin folder  
| /robots.txt: Robots file  
| /config/: Potentially interesting directory w/ listing on 'apache/2.4.7 (ubuntu)'  
| /docs/: Potentially interesting directory w/ listing on 'apache/2.4.7 (ubuntu)'  
|\_ /external/: Potentially interesting directory w/ listing on 'apache/2.4.7 (ubuntu)'  
| http-slowloris-check:   
| VULNERABLE:  
| Slowloris DOS attack  
| State: LIKELY VULNERABLE  
| IDs: CVE:CVE-2007-6750  
| Slowloris tries to keep many connections to the target web server open and hold  
| them open as long as possible. It accomplishes this by opening connections to  
| the target web server and sending a partial request. By doing so, it starves  
| the http server's resources causing Denial Of Service.  
|   
| Disclosure date: 2009-09-17  
| References:  
| <https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2007-6750>  
|\_ <http://ha.ckers.org/slowloris/>  
|\_http-stored-xss: Couldn't find any stored XSS vulnerabilities.  
  
  
