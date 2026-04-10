# Level 4 - Level 5
The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the “reset” command .
# Goal                  
To find the only human-readable file in the inhere directory

# Login credentials
```
ssh bandit4@bandit.labs.overthewire.org -p 2220

--2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
```

# Command  
```
 file ./inhere/*   
 cat ./inhere/./-file07
```
# Explanation    
file command is used to identify the file type . Among all the files only one file will be human-readable (ASCII text) and then we use cat command to read it


# Password        
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
