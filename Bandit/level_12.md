# Level 11 - Level 12
The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

# Goal              
To decode a file where letters are rotated by 13 positions (ROT13)
# Login credentials
```
ssh bandit11@bandit.labs.overthewire.org -p 2220

--dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```

# Command     
```
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

# Explanation   
tr command is used for character translation. ROT13 shifts letters by 13 positions

# Password       
7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
