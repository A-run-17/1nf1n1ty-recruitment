# Level 30 - Level 31
There is a git repository at ssh://bandit30-git@bandit.labs.overthewire.org/home/bandit30-git/repo via the port 2220. The password for the user bandit30-git is the same as for the user bandit30.

From your local machine (not the OverTheWire machine!), clone the repository and find the password for the next level. This needs git installed locally on your machine.


# Goal               
To check git tags

# Login credentials
```
ssh bandit30@bandit.labs.overthewire.org -p 2220

--qp30ex3VLz5MDG1n91YowTv4Q8l7CDZL
```

# Command  
```
git clone ssh://bandit30-git@localhost/home/bandit30-git/repo 
git tag  
git show <tag>
```

# Explanation  
Password stored in a tag

# Password      
fb5S2xb7bRyFmAvQYQGEqsbhVyJqhnDy
                                                                          
