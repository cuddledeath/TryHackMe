# Task 5: Find Flags!

  
#1 Flag1? (Only submit the flag contents {CONTENTS})  
cd C:/  
cat flag1.txt  
flag{access\_the\_machine}  
access\_the\_machine  
  
#2 Flag2? *Errata: Windows really doesn't like the location of this flag and can occasionally delete it. It may be necessary in some cases to terminate/restart the machine and rerun the exploit to find this flag. This relatively rare, however, it can happen.  
  
cd C:/Windows/System32/config  
cat flag2.txt  
flag{sam\_database\_elevated\_access}  
  
sam\_database\_elevated\_access  
  
#3 flag3?  
  
search -f flag*.txt  
C:\Users\Jon\Documents\flag3.txt  
cat C:\\Users\\Jon\\Documents\\flag.txt  
flag{admin\_documents\_can\_be\_valuable}  
  
admin\_documents\_can\_be\_valuable