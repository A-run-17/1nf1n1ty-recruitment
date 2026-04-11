# Natas 27 - Natas 28
    Username  : natas28
    Password  : 1JNwQM1Oi6J6j1k49Xyw7ZN6pXMQInVj
    URL       : http://natas28.natas.labs.overthewire.org

# Solution 
The application is searching for jokes in database containing the word we search for.

It is sending request to search.php with an encrypted query

    http://natas28.natas.labs.overthewire.org/search.php/?query=G%2BglEae6W%2F1XjA7vRm21nNyEco%2Fc%2BJ2TdR0Qp8dcjPKI2nqdSIqg8bRBxCLXlTEXrDuHHBxEg4a0XNNtno9y9GVRSbu6ISPYnZVBfqJ%2FOns%3D

It seems like base64 encoded, but is encrypted.

<img width="940" height="398" alt="image" src="https://github.com/user-attachments/assets/e2fcf3a9-01a2-40a8-9c6d-a8f7ef421774" />

When normal text is sent as query parameter, it shows error related to padding, which hints towards the Block cipher.

<img width="919" height="319" alt="image" src="https://github.com/user-attachments/assets/401de9ff-6ce3-403f-a053-b632b8d3cac3" />

when some valid sequence is entered : 
           
      G+glEae6W/1XjA7vRm21nNyEco/c+J2TdR0Qp8dcjPLof/YMma1yzL2UfjQXqQEop3600aq+C10FxP/mrBQjq0eOsaH+JhosbBUGEQmz/to=

      G+glEae6W/1XjA7vRm21nNyEco/c+J2TdR0Qp8dcjPKriAqPE2++UYlniRMkobB1vfoQV0xoUVz5bypVRFkZR5BPSyq/LC12hqpypTFRyXA=
    
      G+glEae6W/1XjA7vRm21nNyEco/c+J2TdR0Qp8dcjPKxMKUxvsiccFITv6XJZnrHSHmaB7HSm1mCAVyTVcLgDq3tm9uspqc7cbNaAQ0sTFc=
    
      G+glEae6W/1XjA7vRm21nNyEco/c+J2TdR0Qp8dcjPIvUp0m0suf6Me06CS3bWodmi4rXbbzHxmhT3Vnjq2qkEJJuT5N6gkJR5mVucRLNRo=

This hints toward the ECB encryption. The initial encrypted block are some text that are pre-pended to our search input. The encrypted query might be formed by this:

     Default Prepended Text + Our Input + Padding to match the predefined block size

Now checking for block size by increasing the input size . 

<img width="323" height="467" alt="image" src="https://github.com/user-attachments/assets/f43e2d5d-66da-4a82-94dc-82962ada100c" />


Here the Encrypted query length is increased by 32 bytes. The length remain same for 16 characters in input length .

The jump from 160 to 192 at input length 13 is due to the pre-pended characters to our input.

Input Block size = 16 characters

Encrypted Block size = 32 bytes.

Now lets see if we can get encrypted block to same sequence of 32 bytes for consecutive block.

The first two blocks are same for all request. After the input of 10 a , the 3rd block also starts to repeat. So it contains the prepended 6 characters + 10 'a's .

At input length 9 there is 1 character padding at the end

After 10 character input a new block is added with one a and 15 padding character.

If we can fill the remaining blocks with with our input, then next block of bytes will also start to repeat.

<img width="592" height="418" alt="image" src="https://github.com/user-attachments/assets/7e39bb9d-2e94-402c-9377-490527aae9cc" />

Now the repeating block b39038c28df79b65d26151df58f7eaa3 represents 16 a characters.

After next 16 character, next block also start to repeat.

2 blocks with a s.

<img width="546" height="537" alt="image" src="https://github.com/user-attachments/assets/eb7d87f5-6a2f-4917-8edf-c27411eea3ee" />

If we try to inject SQL query in the application it is escaped and is searched as normal text.

Response for searching ' :

<img width="704" height="361" alt="image" src="https://github.com/user-attachments/assets/499487b1-02db-4b45-9f06-ac52ec4328e8" />

To verify it we can send crafted input so that the escaping increases the blocks of bytes in the encrypted query.

When 12 a are sent the size is 160. But when 11 a and 1 ' is sent the size is 192. So this is adding \ character before the ' character.
Our input is divided into blocks and then individual block is encrypted separately due to use of ECB encryption. The escaping is done when input is supplied. The application work flow is like.
 
    input ⇒ escaping SQL-i characters ⇒ encrypt individual block ⇒ combine encrypted blocks ⇒ encrypted query

    encrypted query ⇒ decryption block by block ⇒ combine the decrypted string ⇒ run the SQL query to fetch the joke.

We assume ' is converted to \' and then encrypted.

If we can insert the ' character at the end of the block \ is inserted at the end of the block and the ' character is pushed to the next block.

Since individual blocks are decrypted individually and then the resulting text is combined, we replace the encrypted byte block with \ at the end with encrypted byte block with normal character at the end.

This will result in text with no escaping of the ' character and can execute the arbitrary SQL injection code which can be used to obtain the password for the next level.

We know in the third block there is space for 10 characters, So putting 9 a and ' will replace ' with \ and push ' to the next block.

Using this python script :
```
data = {"query": "a"*9+"' UNION SELECT ALL password from
users; #"}
data_length = len(data['query' ])

res = requests.post (url=url, data=data, auth = (username,
password) )
encrypted_raw = binascii.hexlify(base64.b64decode (unquote(res
.url[60:]) ) ) . decode ()
encrypted_raw_length = len(encrypted_raw)
print("input Length: "+str(data_length)+" Encrypted query
Length: "+str(encrypted_raw_length)+"\n")
block_size = 32
for i in range(encrypted_raw_length//block_size):
print(encrypted_raw[block_size*i:block_size*(i+1)])
print("="*40)
```
<img width="997" height="393" alt="image" src="https://github.com/user-attachments/assets/ef811266-2535-454c-84f0-ad56f5437b06" />

If we replace the 3rd block with encrypted byte block with xxxxxxaaaaaaaaaa (10 a ), the encrypted query is a valid one but without a escaping \ .

<img width="1674" height="783" alt="image" src="https://github.com/user-attachments/assets/241cad30-5ac5-4c0b-9ffc-84ad56f6d278" />

URL encode the payload then provide to the search query to get the password for the next level.

# Password 
       pc0w0Vo0KpTHcEsgMhXu2EwUzyYemPno

       









      



