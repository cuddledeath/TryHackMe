In order to follow up along with the task content and apply what is given in this room, you need to start the attached machine by using the green Start Machine button in this task, and wait a few minutes for it to boot up. To access the attached machine, you can either use the split in browser view or connect through the RDP.

If you prefer to connect through the Remote Desktop Protocol (RDP), first make sure you are connected to the VPN. Then an RDP client is required to connect to the attached Windows 10 machine. You can connect using the xfreerdp tool, which is available on the TryHackMe AttackBox.

To connect  via xfreerdp use the following command:

Terminal

```shell-session
user@machine$ xfreerdp /v:MACHINE_IP /u:thm /p:TryHackM3 +clipboard
```

The username: thm and the password: TryHackM3   

Answer the questions below

Deploy the attached Windows machine and connect to it via the RDP client. Once this is done, move to the next task.