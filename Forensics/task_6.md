# Task 6
 Book ciper 


# Method Used

When we check the output of the previous step we got a bunch of things 

          A book code as a  hash
          Some integers with the instructions
          And a PGP signature
          
Though it is mentioned as SHA1 hash , After brute forcing method we found out that it is a 
SHA512 hash . So upon using an online hash cracking application we got the web address
 
       Link  :  https://pastebin.com/6FNiVLh5

In that web address we can see some proverbs . After various trails we found the clue which is nothing 
but the integers we got while analyzing the second image . (Ex : I 13:5 , I 23 : -1 .. etc) .  For example

      I 13:5   means 13th line 5 character (Excluding spacebars )
      I 23:-1  means 23rd line -1 character (3)

Like this if we did for the entire integers we will again get a web address 
 
      Link : https://bit.ly/39pw2NH

# Found  

     hash          :  SHA512
     cracked hash  :  https://pastebin.com/6FNiVLh5
     decodec  Link : https://bit.ly/39pw2NH
