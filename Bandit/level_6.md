# Level 5 - Level 6
The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:

       human-readable
       
       1033 bytes in size 
       
       not executable

# Goal                  
To find a file with size 1033 bytes , not executable and human readable

# Login credentials
```
ssh bandit5@bandit.labs.overthewire.org -p 2220

--4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
```

# Command       
```
find . -type f -size 1033c ! -executable

```
# Explanation    
find command is used to search files based on conditions . Here we are searching for a file (-type f) with size 1033 bytes (-size 1033c) and not executable (! -executable) .


# Password        
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
