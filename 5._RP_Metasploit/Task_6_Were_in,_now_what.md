# Task 6: We're in, now what?

  
#1 First things first, our initial shell/process typically isn't very stable. Let's go ahead and attempt to move to a different process. First, let's list the processes using the command 'ps'. What's the name of the spool service?  
spoolsv.exe  
  
#2 Let's go ahead and move into the spool process or at least attempt to! What command do we use to transfer ourselves into the process? This won't work at the current time as we don't have sufficient privileges but we can still try!  
migrate  
  
#3 Well that migration didn't work, let's find out some more information about the system so we can try to elevate. What command can we run to find out more information regarding the current user running the process we are in?  
getuid  
  
#4 How about finding more information out about the system itself?  
sysinfo  
  
#5 This might take a little bit of googling, what do we run to load mimikatz (more specifically the new version of mimikatz) so we can use it?   
load kiwi  
  
#6 Let's go ahead and figure out the privileges of our current user, what command do we run?  
getprivs  
  
#7 What command do we run to transfer files to our victim computer?  
upload  
  
#8 How about if we want to run a Metasploit module?  
run  
  
#9 A simple question but still quite necessary, what command do we run to figure out the networking information and interfaces on our victim?  
ipconfig  
  
#10 Let's go ahead and run a few post modules from Metasploit. First, let's run the command `run post/windows/gather/checkvm`. This will determine if we're in a VM, a very useful piece of knowledge for further pivoting.  
  
#11 Next, let's try: `run post/multi/recon/local\_exploit\_suggester`. This will check for various exploits which we can run within our session to elevate our privileges. Feel free to experiment using these suggestions, however, we'll be going through this in greater detail in the room `Ice`.  
  
#12 Finally, let's try forcing RDP to be available. This won't work since we aren't administrators, however, this is a fun command to know about: `run post/windows/manage/enable\_rdp`  
  
#13 One quick extra question, what command can we run in our meterpreter session to spawn a normal system shell? 

