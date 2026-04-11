# Natas 10 - Natas 11
    Username : natas11
    Password : UJdqkK1pTu6VLt9UHWAgRZz6sVUZ3lEk
    URL      :  http://natas11.natas.labs.overthewire.org
    
# Solution

From the source page we can find that 
```
<?

$defaultdata = array( "showpassword"=>"no", "bgcolor"=>"#ffffff");

function xor_encrypt($in) {
    $key = '<censored>';
    $text = $in;
    $outText = '';

    // Iterate through each character
    for($i=0;$i<strlen($text);$i++) {
    $outText .= $text[$i] ^ $key[$i % strlen($key)];
    }

    return $outText;
}

function loadData($def) {
    global $_COOKIE;
    $mydata = $def;
    if(array_key_exists("data", $_COOKIE)) {
    $tempdata = json_decode(xor_encrypt(base64_decode($_COOKIE["data"])), true);
    if(is_array($tempdata) && array_key_exists("showpassword", $tempdata) && array_key_exists("bgcolor", $tempdata)) {
        if (preg_match('/^#(?:[a-f\d]{6})$/i', $tempdata['bgcolor'])) {
        $mydata['showpassword'] = $tempdata['showpassword'];
        $mydata['bgcolor'] = $tempdata['bgcolor'];
        }
    }
    }
    return $mydata;
}

function saveData($d) {
    setcookie("data", base64_encode(xor_encrypt(json_encode($d))));
}

$data = loadData($defaultdata);

if(array_key_exists("bgcolor",$_REQUEST)) {
    if (preg_match('/^#(?:[a-f\d]{6})$/i', $_REQUEST['bgcolor'])) {
        $data['bgcolor'] = $_REQUEST['bgcolor'];
    }
}

saveData($data);



?>
```
In this challenge, the code seems to add the color of the background into our cookie. 
Also, the cookie contains the field showpassword set to no. 
If we modify the value to yes we will get the password. 
However, we don’t have the key for the xor_encrypt() function.
As the algorithm used is XOR and we know the plaintext and ciphertext values of the cookie we can recover the key. 
This is due to the fact that ciphertext ^ plaintext = key, it’s called known-plaintext attack. 
```
import base64
import json

cookie = "HmYkBwozJw4WNyAAFyB1VUcqOE1JZjUIBis7ABdmbU1GIjEJAyIxTRg="

def xor(data, key):
    return bytes([data[i] ^ key[i % len(key)] for i in range(len(data))])

default_data = { "showpassword": "no" , "bgcolor": "#ffffff" }

default_json = json.dumps(default_data, separators=(',', ':'))
decoded_cookie = base64.b64decode(cookie)
key = xor(decoded_cookie, default_json.encode())


for i in range(1, len(key)):
    if key[:i] * (len(key) // i) == key[:i * (len(key) // i)]:
        key = key[:i]
        break

print("Key found:", key)

new_data = { "showpassword": "yes" , "bgcolor": "#ffffff" }

new_json = json.dumps(new_data, separators=(',', ':'))
new_cookie = xor(new_json.encode(), key)
final_cookie = base64.b64encode(new_cookie).decode()

print("New cookie:", final_cookie)
```
The above python script takes the current cookie and that default data and perform xor encryption to find the key and then the key is xor'rd with the new data as we wanted and the final base64 decoded cookie is given as the output

# Password 
     yZdkjAYZRd3R7tq7T5kXMjMJlOIkzDeB
     

