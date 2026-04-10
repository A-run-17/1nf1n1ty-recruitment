# Level 14 - Level 15
The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.

# Goal              
To submit the  current Password to a port using netcat
# Login credentials
```
ssh bandit14@bandit.labs.overthewire.org -p 2220

--MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
```

# Command     
```
echo 'MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS' | nc localhost 30000
```

# Explanation  
nc (netcat) is used to connect to a port and send data . Here we are connecting to localhost using the port 30000 

# Password      
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo

