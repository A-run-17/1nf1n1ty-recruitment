# Level 24 - Level 25
A daemon is listening on port 30002 and will give you the password for bandit25 if given the password for bandit24 and a secret numeric 4-digit pincode. There is no way to retrieve the pincode except by going through all of the 10000 combinations, called brute-forcing.
You do not need to create new connections each time

# Goal                
To brute force a 4 digit PIN and send it to the port number 30002 with our ci=urrent Password 

```
ssh bandit24@bandit.labs.overthewire.org -p 2220

--gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8
```

# Command      :
```
nano /tmp/for_loop.sh
write the shell script :
for i in {0000..9999}; 
do
   echo "YOUR_Password $i"
done | nc localhost 30002
```

# Explanation    
loop tries all combinations of 4 digit PIN and sends to service which is stored in a file . change the permimssion of the file and run


# Password       
iCi86ttT4KSNe1armKiwbQNmB3YJP3q4
