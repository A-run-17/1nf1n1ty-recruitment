# Level 10 - Level 11
The password for the next level is stored in the file data.txt, which contains base64 encoded data

# Goal               
To decode base64 encoded data
# Login credentials
```
ssh bandit10@bandit.labs.overthewire.org -p 2220

--FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
```

# Command      
```
base64 -d data.txt
```

# Explanation   
base64 -d is used to decode base64 encoded content . -d stands for decoding . 

# Password       
dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
