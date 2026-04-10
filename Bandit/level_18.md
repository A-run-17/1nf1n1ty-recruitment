# Level 17 - Level 18
There are 2 files in the homedirectory: passwords.old and passwords.new. The password for the next level is in passwords.new and is the only line that has been changed between passwords.old and passwords.new
NOTE: if you have solved this level and see ‘Byebye!’ when trying to log into bandit18, this is related to the next level, bandit19

# Goal               
To find the difference between two files

# Login credentials
```
ssh bandit17@bandit.labs.overthewire.org -p 2220

--RSA Private Key
```

# Command      
```
diff Passwords.old Passwords.new
```

# Explanation   
diff command is used to show the difference between two files 

# Password       
x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
