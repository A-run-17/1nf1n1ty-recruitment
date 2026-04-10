# Level 7 - Level 8
The password for the next level is stored in the file data.txt next to the word millionth

# Login credentials
```
ssh bandit7@bandit.labs.overthewire.org -p 2220

--HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
```

# Goal               
To find the Password stored in the file data.txt next to the word millionth

# Command  
```
cat data.txt | grep "millionth"
```

# Explanation   
grep command is used to search for a specific word inside a file . the pipe ( | ) symbol is used to give the output of the first command as a argument to the second command

# Password       
dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
