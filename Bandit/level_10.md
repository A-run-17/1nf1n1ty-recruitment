# Level 9 - Level 10
The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.

# Goal                
To find the Password in data.txt among binary data

# Login credentials
```
ssh bandit9@bandit.labs.overthewire.org -p 2220

--4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```

# Command        
```
strings data.txt | grep "="
```

# Explanation    
strings extracts readable text from binary files and grep is used to filter the required line

# Password       
FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
