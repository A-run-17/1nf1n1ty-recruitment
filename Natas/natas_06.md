# Natas 5 - Natas 6
    Username  : natas6
    Password  : 0RoJwHdSKWFTYR5WuiAewauSuNaBXned
    URL       : http://natas6.natas.labs.overthewire.org

# Solution
In the source paga we can find the function :

```
include "includes/secret.inc";

    if(array_key_exists("submit", $_POST)) {
        if($secret == $_POST['secret']) {
        print "Access granted. The password for natas7 is <censored>";
    } else {
        print "Wrong secret";
    }
    }
```
Using the information from the function , we can visit includes/secret.inc folder there we can find :
```
<?
$secret = "FOEIUWGHFEEUHOFUOIU";
?>
```
Use the secret as input to the mainpage and get the password

# Password
     bmg8SvU1LizuWjx3y7xkNERkHxGre0GS
