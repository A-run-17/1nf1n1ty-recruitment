# Natas 7 - Natas 8
    Username  : natas8
    password  : xcoXLmzMkoIP9D7hlgPlh9XD7OgLAe5Q
    URL       : http://natas8.natas.labs.overthewire.org
# Solution

On visiting the source of the page we can find a function 
```
<?

$encodedSecret = "3d3d516343746d4d6d6c315669563362";

function encodeSecret($secret) {
    return bin2hex(strrev(base64_encode($secret)));
}

if(array_key_exists("submit", $_POST)) {
    if(encodeSecret($_POST['secret']) == $encodedSecret) {
    print "Access granted. The password for natas9 is <censored>";
    } else {
    print "Wrong secret";
    }
}
?>
```
We shold decode the encoded Secret in same order encoded . For this this basic decoding we can use linux commands .

        echo '3d3d516343746d4d6d6c315669563362'| xxd -r -p | rev | base64 -d
Enter the decoded Secret in the input of the main page to obtain the nect level password .

# Password
       ZE1ck82lmdGIoErlhQgWND6j2Wzz6b6t
       
