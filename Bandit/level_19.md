# Level 18 - Level 19
The password for the next level is stored in a file readme in the homedirectory. Unfortunately, someone has modified .bashrc to log you out when you log in with SSH.

# Goal              
To login but shell immediately logs out

# Login credentials
```
ssh bandit18@bandit.labs.overthewire.org -p 2220

--x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
```

# Command     
```
ssh bandit18@bandit.labs.overthewire.org -p 2220 "cat readme"
```

# Explanation  
Since we cannot login we use a command with the ssh command which runs as soon as the system is logined so we get the output of the command even though we can not able login . The command nees to be runed inside ig given within " " .

# Password     
cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8
