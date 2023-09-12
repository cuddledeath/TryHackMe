# Task 7: Makin' Cisco Proud

  
#1 Let's go ahead and run the command `run autoroute -h`, this will pull up the help menu for autoroute. What command do we run to add a route to the following subnet: 172.18.1.0/24? Use the -n flag in your answer.  
  
run autoroute -s 172.18.1.0 -f 255.255.255.0  
  
  
  
#2 Additionally, we can start a socks4a proxy server out of this session. Background our current meterpreter session and run the command `search server/socks4a`. What is the full path to the socks4a auxiliary module?  
  
auxiliary/server/socks4a  
  
#3 Once we've started a socks server we can modify our /etc/proxychains.conf file to include our new server. What command do we prefix our commands (outside of Metasploit) to run them through our socks4a server with proxychains?  
  
proxychains