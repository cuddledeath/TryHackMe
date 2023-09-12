# Task 3: Escalate

  
#1 If you haven't already, background the previously gained shell (CTRL + Z). Research online how to convert a shell to meterpreter shell in metasploit. What is the name of the post module we will use? (Exact path, similar to the exploit we previously selected)   
  
post/multi/manage/shell\_to\_meterpreter  
  
#2 Select this (use MODULE\_PATH). Show options, what option are we required to change? (All caps for answer)  
  
SESSION  
  
#3 Set the required option, you may need to list all of the sessions to find your target here.   
  
set SESSION 1  
exploit  
sessions -i 2  
  
#4 Run! If this doesn't work, try completing the exploit from the previous task once more.  
  
#5 Once the meterpreter shell conversion completes, select that session for use.  
  
#6 Verify that we have escalated to NT AUTHORITY\SYSTEM. Run getsystem to confirm this. Feel free to open a dos shell via the command 'shell' and run 'whoami'. This should return that we are indeed system. Background this shell afterwards and select our meterpreter session for usage again.   
  
#7 List all of the processes running via the 'ps' command. Just because we are system doesn't mean our process is. Find a process towards the bottom of this list that is running at NT AUTHORITY\SYSTEM and write down the process id (far left column).  
ps  
  
#8 Migrate to this process using the 'migrate PROCESS\_ID' command where the process id is the one you just wrote down in the previous step. This may take several attempts, migrating processes is not very stable. If this fails, you may need to re-run the conversion process or reboot the machine and start once again. If this happens, try a different process next time.   
migrate -n winlogon.exe  
