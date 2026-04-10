# Level 15 - Level 16 
The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL/TLS encryption.
Helpful note: Getting “DONE”, “RENEGOTIATING” or “KEYUPDATE”? Read the “CONNECTED COMMANDS” section in the manpage.

# Goal               
To connect using SSL to a port
# Login credentials
```
ssh bandit15@bandit.labs.overthewire.org -p 2220

--8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
```

# Command  
```
echo "8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo" | openssl s_client -quiet -connect localhost:30001
```

# Explanation   
openssl s_client is used to connect to SSL encrypted services . -quite will remove unwanted information

# Password       
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
