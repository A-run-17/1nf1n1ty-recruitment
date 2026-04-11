# Level 28 - Level 29
There is a git repository at ssh://bandit28-git@bandit.labs.overthewire.org/home/bandit28-git/repo via the port 2220. The password for the user bandit28-git is the same as for the user bandit28.

From your local machine (not the OverTheWire machine!), clone the repository and find the password for the next level. This needs git installed locally on your machine.

# Goal               
To check git history for Password

# Login credentials
```
ssh bandit28@bandit.labs.overthewire.org -p 2220

--Yz9IpL0sBcCeuG7m9uQFt8ZNpS4HZRcN
```
# Command    
```
git clone ssh://bandit28-git@localhost/home/bandit28-git/repo  
git log -p  
```

# Explanation  
Password was removed but exists in previous commit .  -p option in git command is used to find all the previous commits

# Password      
4pT1t5DENaYuqnqvadYs1oE4QLCdjmJ7
