# XOR Starter

XOR is a bitwise operator which returns 0 if the bits are the same, and 1 otherwise. In textbooks the XOR operator is denoted by ⊕, but in most challenges and programming languages you will see the caret ^ used instead.

        A   ^ 	B  	 Output
        0	    0     0
        0    	1	  1
        1    	0 	  1
        1    	1     0

For longer binary numbers we XOR bit by bit: 0110 ^ 1010 = 1100. We can XOR integers by first converting the integer from decimal to binary. We can XOR strings by first converting each character to the integer representing the Unicode character.

Given the string label, XOR each character with the integer 13. Convert these integers back to a string and submit the flag as crypto{new_string}.

# Hint 
The Python pwntools library has a convenient xor() function that can XOR together data of different types and lengths. But first, you may want to implement your own function to solve this.

# Python Script

     from pwnlib.util.fiddling import xor
     a = 'lable'
     decode = ''
     key = 13
     for i in range(len(a)):
        x = xor(a[i] , key)
        decode += chr(x)

      print(decode)

# Solution

The string " lable " is xor compared with the integer 13 and and the final flag is captured . For xor comparison we are using a library called pwntools

    Flag   :   crypto{aloah}
