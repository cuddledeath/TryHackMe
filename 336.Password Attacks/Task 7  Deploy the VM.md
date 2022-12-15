Deploy the attached VM to apply the knowledge we discussed in this room. The attached VM has various online services to perform password attacks on. Custom wordlists are needed to find valid credentials.

We recommend using https://clinic.thmredteam.com/ to create your custom wordlist.

To generate your wordlist using cewl against the website:

John Rules

```shell-session
user@machine$ cewl -m 8 -w clinic.lst https://clinic.thmredteam.com/  
```

Note that you will also need to generate a username wordlist as shown in Task 3: Password Profiling #1 for the online attack questions.

Answer the questions below

Get your pentest weapons ready to attack 10.10.105.48.