# Level 13 - Level 14
The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Look at the commands that logged you into previous bandit levels, and find out how to use the key for this level.

# Goal              
To use SSH private key to login

# Login credentials
```
ssh bandit13@bandit.labs.overthewire.org -p 2220

--FO5dwFsc0cbaUvavEWKLjAsuGm6hPk0x
```

# Command    
```
scp -P 2220 bandit13@bandit.labs.overthewire.org:/home/bandit13/sshkey.private .
ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
cat /etc/bandit_pass/bandit14
```

# Explanation   
scp command is used to transfer the ssh key to our own computer and change the permission . -i is used to specify private key for authentication instead of Password . After getting inside the bandit14 terminal we can find the password of bandit14 or we can just use the rsa key for login

# Password       
MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
