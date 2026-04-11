# Level 21 - Level 22
A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.


# Goal              
To find a cronjob running and retrieve Password

# Login credentials
```
ssh bandit21@bandit.labs.overthewire.org -p 2220

--EeoULMCra2q0dSkYj561DX7s1CpBuOBt
```

# Command     
```
cat /etc/cron.d/cronjob_bandit22

 cat /usr/bin/cronjob_bandit22.sh

cat /tmp/filename
```

# Explanation   
cronjobs run automatically. By reading the script we find where the Password is stored

# Password       
tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q
