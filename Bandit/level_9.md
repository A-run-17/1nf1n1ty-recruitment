# Level 8 - Level 9
The password for the next level is stored in the file data.txt and is the only line of text that occurs only once

# Goal               
To find the Password which is the only line that occurs once in the file data.txt

# Login credentials
```
ssh bandit8@bandit.labs.overthewire.org -p 2220

--dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```
 
# Command
```
sort data.txt | uniq -u
```

# Explanation    
sort is used to sort the data and uniq -u shows only unique lines .  uniq only removes adjacent duplicates so uniq is used with sort.

# Password        
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
