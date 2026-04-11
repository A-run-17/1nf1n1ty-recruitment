# XOR Properties
In the last challenge, you saw how XOR worked at the level of bits. In this one, we're going to cover the properties of the XOR operation and then use them to undo a chain of operations that have encrypted a flag. Gaining an intuition for how this works will help greatly when you come to attacking real cryptosystems later, especially in the block ciphers category.

There are four main properties we should consider when we solve challenges using the XOR operator

     Commutative   :  A ⊕ B = B ⊕ A
     Associative   :  A ⊕ (B ⊕ C) = (A ⊕ B) ⊕ C
     Identity      :  A ⊕ 0 = A
     Self-Inverse  :  A ⊕ A = 0
Let's break this down. Commutative means that the order of the XOR operations is not important. Associative means that a chain of operations can be carried out without order (we do not need to worry about brackets). The identity is 0, so XOR with 0 "does nothing", and lastly something XOR'd with itself returns zero.

Let's put this into practice! Below is a series of outputs where three random keys have been XOR'd together and with the flag. Use the above properties to undo the encryption in the final line to obtain the flag.

 ```KEY1 = a6c8b6733c9b22de7bc0253266a3867df55acde8635e19c73313
KEY2 ^ KEY1 = 37dcb292030faa90d07eec17e3b1c6d8daf94c35d4c9191a5e1e
KEY2 ^ KEY3 = c1545756687e7573db23aa1c3452a098b71a7fbf0fddddde5fc1
FLAG ^ KEY1 ^ KEY3 ^ KEY2 = 04ee9855208a2cd59091d04767ae47963170d1660df7f56f5faf
 ```

# Hint
Before you XOR these objects, be sure to decode from hex to bytes.

# Python Script
 ```
def xor(a, b):
    return bytes(x ^ y for x, y in zip(a, b))

key1 = bytes.fromhex("a6c8b6733c9b22de7bc0253266a3867df55acde8635e19c73313")
k2_xor_k1 = bytes.fromhex("37dcb292030faa90d07eec17e3b1c6d8daf94c35d4c9191a5e1e")
k2_xor_k3 = bytes.fromhex("c1545756687e7573db23aa1c3452a098b71a7fbf0fddddde5fc1")
flag_xor_all = bytes.fromhex("04ee9855208a2cd59091d04767ae47963170d1660df7f56f5faf")

key2 = xor(k2_xor_k1, key1)
key3 = xor(k2_xor_k3, key2)

flag = xor(flag_xor_all, xor(key1, xor(key2, key3)))
print(flag)
 ```

# Solution
This time we are not using the built-in function we are gooing to write xor function manualy . From the given information

     Key 2 ^ Key 1 = tmp_key 
     
Xor compare with Key 1 both sides
     
     Key 2 ^ Key 1 ^ Key 1 = tmp_key ^ Key 1

From the properties

     Key 2 ^ 0 = tmp_key ^ Key 1
     Key 1 ^ tmp_key = Key 2

Like this all the keys are found and the final flag is obtained

    Flag  :   crypto{x0r_i5_ass0c1at1v3}
