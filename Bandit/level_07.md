# Level 6 - Level 7
The password for the next level is stored somewhere on the server and has all of the following properties:

      owned by user bandit7
      
      owned by group bandit6 
      
      33 bytes in size
      
# Goal              
To find a file somewhere on the server owned by user bandit7 and group bandit6 and size 33 bytes

# Login credentials
```
ssh bandit6@bandit.labs.overthewire.org -p 2220

--HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
```

# Command     
```
find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

# Explanation   
/ means searching the whole system for a file whose user is bandit7 and group is bandit6 and size is 33 bytes in size . 2>/dev/null is used to remove permission denied errors

# Password       
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
