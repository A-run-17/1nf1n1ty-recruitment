# Level 23 - Level 24
A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

NOTE: This level requires you to create your own first shell-script. This is a very big step and you should be proud of yourself when you beat this level!

NOTE 2: Keep in mind that your shell script is removed once executed, so you may want to keep a copy around…

# Login credentials
```
ssh bandit23@bandit.labs.overthewire.org -p 2220

--0Zf11ioIjMVN551jX3CmStKLYqjk54Ga
```
# Goal             
To write a script and get executed by cronjob

# Command   
```
cat /etc/cron.d/cronjob_bandit24  
cat /usr/bin/cronjob_bandit24.sh
mkdir /tmp/Password 
nano code.sh : 
#!/bin/bash
   cat /etc/bandit_pass/bandit24 > /tmp/Password/newPassword.txt
chmod 700 code.sh
./ code.sh
```

# Explanation   
cronjob executes scripts from a directory. We place our script and get Password written to /tmp . Before executing the file the permissions need to be changed

# Password     
gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8
