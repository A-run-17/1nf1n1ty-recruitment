# Level 12 - Level 13
The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work. Use mkdir with a hard to guess directory name. Or better, use the command “mktemp -d”. Then copy the datafile using cp, and rename it using mv (read the manpages!)
# Goal                 
To extract data from a file multiple times compressed

# Login credentials
```
ssh bandit12@bandit.labs.overthewire.org -p 2220

--7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```

# Command  
```
xxd -r data.txt > data.bin , file data.bin , 
gunzip filename (to unzip using gzip) , 
bunzip2 filename (to unzip using bunzip) ,    
tar -xf filename (to unzip using tar)
```

# Explanation      
First we reverse hex dump using xxd -r then identify file type and  using the file command know the type then repeatedly decompress using appropriate tools like gzip , bzip2 , tar

# Password         
FO5dwFsc0cbaUvavEWKLjAsuGm6hPk0x
