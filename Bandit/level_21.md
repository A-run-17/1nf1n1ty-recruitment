# Level 20 - Level 21
There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).

NOTE: Try connecting to your own network daemon to see if it works as you think

# Goal              
To connect to a port and send the current Password TO gain the Password for next level

# Login credentials
```
ssh bandit20@bandit.labs.overthewire.org -p 2220

--0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
```

# Command
```
echo "0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO" | nc -nvlp 2000 &   

./suconnect 2000 "0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO"
```

# Explanation  
suconnect listens on a port and checks if the correct Password is sent. We use netcat to send the Password  . & is used for running it in background

# Password     
EeoULMCra2q0dSkYj561DX7s1CpBuOBt
