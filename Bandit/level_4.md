# Level 3 - Level 4 
The password for the next level is stored in a hidden file in the inhere directory.

# Goal             
To read a hidden file in the inhere directory.

# Login credentials
```
ssh bandit3@bandit.labs.overthewire.org -p 2220

--MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
```

# Command  
```
ls -al

cat .filename
```
# Explanation    
Usually in Linux hidden files start with . in their filename . To list the file we use the -al option in the ls command  to view the hidden files . To read the content in the hidden file we use cat .filename command


# Password        
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
