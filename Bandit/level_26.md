# Level 25 - Level 26
Logging in to bandit26 from bandit25 should be fairly easy… The shell for user bandit26 is not /bin/bash, but something else. Find out what it is, how it works and how to break out of it.

NOTE: if you’re a Windows user and typically use Powershell to ssh into bandit: Powershell is known to cause issues with the intended solution to this level. You should use command prompt instead.

# Goal               
To login but shell is restricted

```
ssh bandit25@bandit.labs.overthewire.org -p 2220

-- iCi86ttT4KSNe1armKiwbQNmB3YJP3q4
```

# Command     
```

ssh -i sshkey.private bandit26@localhost -p 2220
press v to go to vim 
: set shell = /bin/bash
: shell  
cat /etc/bandit_pass/bandit26
```
 
# Explanation  
shell exits immediately. Resize terminal to trigger pager and escape using vim because it is using more command . declear shell = /bin/bash and execute set to get into the terminal

# Password     
s0773xxkk0MXfdqOfPRVr9L3jJBUOgCZ
