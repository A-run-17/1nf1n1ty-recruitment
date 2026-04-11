# Level 22 - Level 23
A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

NOTE: Looking at shell scripts written by other people is a very useful skill. The script for this level is intentionally made easy to read. If you are having problems understanding what it does, try executing it to see the debug information it prints.

# Goal              
To find Password using another cronjob
# Login credentials
```
ssh bandit22@bandit.labs.overthewire.org -p 2220

--tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q
```


# Command       
```
cat /etc/cron.d/cronjob_bandit23  
cat /usr/bin/cronjob_bandit23.sh
cat /tmp/$(echo "I am user bandit23" | md5sum)
```

# Explanation    
script creates a file in /tmp using hashed filename . We generate the same filename and read it . $ uses the output of the bash commands
 
 #Password       
 0Zf11ioIjMVN551jX3CmStKLYqjk54Ga
