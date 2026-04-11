# Level 29 - Level 30
There is a git repository at ssh://bandit29-git@bandit.labs.overthewire.org/home/bandit29-git/repo via the port 2220. The password for the user bandit29-git is the same as for the user bandit29.

From your local machine (not the OverTheWire machine!), clone the repository and find the password for the next level. This needs git installed locally on your machine.


# Goal              
To check other branches

# Login credentials
 ```
ssh bandit29@bandit.labs.overthewire.org -p 2220

--4pT1t5DENaYuqnqvadYs1oE4QLCdjmJ7
```

# Command   
```
git clone ssh://bandit29-git@localhost/home/bandit29-git/repo , 
git branch -a  
git switch dev  
cat README
```

# Explanation  
Password is stored in another branch . switch the branch and find the Password 

# Password      
qp30ex3VLz5MDG1n91YowTv4Q8l7CDZL
