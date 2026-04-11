# Natas 26 - Natas 27
    Username  : natas27
    Password  : u3RRffXjysjgwFU6b9xa23i6prmUsYne
    URL       : http://natas27.natas.labs.overthewire.org

# Solution

Looking at the source code : 
```
<? 
/* 
CREATE TABLE `users` ( 
  `username` varchar(64) DEFAULT NULL, 
  `password` varchar(64) DEFAULT NULL 
); 
*/ 

function checkCredentials($link,$usr,$pass){ 
  
    $user=mysql_real_escape_string($usr); 
    $password=mysql_real_escape_string($pass); 
     
    $query = "SELECT username from users where username='$user' and password='$password' "; 
    $res = mysql_query($query, $link); 
    if(mysql_num_rows($res) > 0){ 
        return True; 
    } 
    return False; 
} 

function validUser($link,$usr){ 
     
    $user=mysql_real_escape_string($usr); 
     
    $query = "SELECT * from users where username='$user'"; 
    $res = mysql_query($query, $link); 
    if($res) { 
        if(mysql_num_rows($res) > 0) { 
            return True; 
        } 
    } 
    return False; 
} 

function dumpData($link,$usr){ 
     
    $user=mysql_real_escape_string($usr); 
     
    $query = "SELECT * from users where username='$user'"; 
    $res = mysql_query($query, $link); 
    if($res) { 
        if(mysql_num_rows($res) > 0) { 
            while ($row = mysql_fetch_assoc($res)) { 
                // thanks to Gobo for reporting this bug!   
                //return print_r($row); 
                return print_r($row,true); 
            } 
        } 
    } 
    return False; 
} 

function createUser($link, $usr, $pass){ 

    $user=mysql_real_escape_string($usr); 
    $password=mysql_real_escape_string($pass); 
     
    $query = "INSERT INTO users (username,password) values ('$user','$password')"; 
    $res = mysql_query($query, $link); 
    if(mysql_affected_rows() > 0){ 
        return True; 
    } 
    return False; 
} 

if(array_key_exists("username", $_REQUEST) and array_key_exists("password", $_REQUEST)) { 
    $link = mysql_connect('localhost', 'natas27', '<censored>'); 
    mysql_select_db('natas27', $link); 
    

    if(validUser($link,$_REQUEST["username"])) { 
        //user exists, check creds 
        if(checkCredentials($link,$_REQUEST["username"],$_REQUEST["password"])){ 
            echo "Welcome " . htmlentities($_REQUEST["username"]) . "!<br>"; 
            echo "Here is your data:<br>"; 
            $data=dumpData($link,$_REQUEST["username"]); 
            print htmlentities($data); 
        } 
        else{ 
            echo "Wrong password for user: " . htmlentities($_REQUEST["username"]) . "<br>"; 
        }         
    }  
    else { 
        //user doesn't exist 
        if(createUser($link,$_REQUEST["username"],$_REQUEST["password"])){  
            echo "User " . htmlentities($_REQUEST["username"]) . " was created!"; 
        } 
    } 

    mysql_close($link); 
} else { 
?>
```
The username column is VARCHAR(64). MySQL truncates values longer than 64 characters. Also, MySQL string comparison ignores trailing spaces by default.

MySQL will truncate the input to match the maximum field size.

Then if you try to login with the user username and an empty password you’ll get the password! So, theorycally, if you create the following user with an empty password (note the character at the end of the string):

        natas28                                                                                                   x
# Password 
       1JNwQM1Oi6J6j1k49Xyw7ZN6pXMQInVj
