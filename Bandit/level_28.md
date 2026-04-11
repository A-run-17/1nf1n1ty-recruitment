# Level 27 - Level 28
There is a git repository at ssh://bandit27-git@bandit.labs.overthewire.org/home/bandit27-git/repo via the port 2220. The password for the user bandit27-git is the same as for the user bandit27.
From your local machine (not the OverTheWire machine!), clone the repository and find the password for the next level. This needs git installed locally on your machine.

# Goal              
To clone git repository
```
ssh bandit27@bandit.labs.overthewire.org -p 2220

--upsNCc7vzaRDx6oZC6GiR6ERwe1MowGB
```

# Command  
```
git clone ssh://bandit27-git@localhost/home/bandit27-git/repo
cd repo
cat README
```

# Explanation 
git repository is cloned in our local computer and ans the file containing password is read from the repo cloned

# Password     
Yz9IpL0sBcCeuG7m9uQFt8ZNpS4HZRcN
