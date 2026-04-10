# Level 16 - Level 17
The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000. First find out which of these ports have a server listening on them. Then find out which of those speak SSL/TLS and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.
Helpful note: Getting “DONE”, “RENEGOTIATING” or “KEYUPDATE”? Read the “CONNECTED COMMANDS” section in the manpage.

# Goal               
To find the correct port (which is not known) returns SSL certificate 

# Login credentials
```
ssh bandit16@bandit.labs.overthewire.org -p 2220

--kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
```
# Command      
```
nmap -p 31000-32000 -T5 -sV localhost  
echo "kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx" | openssl s_client -quiet -connect localhost:port
```

# Explanation   
nmap is used to scan ports and find open services then use openssl to connect which run the openssl service

# Password      
RSA Private Key
