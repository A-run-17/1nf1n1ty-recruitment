# You either know, XOR you don't
I've encrypted the flag with my secret key, you'll never be able to guess it.

     0e0b213f26041e480b26217f27342e175d0e070a3c5b103e2526217f27342e175d0e077e263451150104

# Hint
Remember the flag format and how it might help you in this challenge!

# Python Script 
 ```
from pwnlib.util.fiddling import xor

data = bytes.fromhex("0e0b213f26041e480b26217f27342e175d0e070a3c5b103e2526217f27342e175d0e077e263451150104")
kk = b'crypto{'

print(xor(data,kk).decode('ascii'))

new_key = b'myXORkey'
print(xor(data,new_key).decode('ascii'))
 ```

# Solution
The key is not given . But we know that the flag will contain crypto{} in it . using the property

    A  ^  B  : C
    A  ^  C  : B

The word crypto is xor'rd with the given string . Then from that we can find the key and then obtain the Flag .

    Flag   :   crypto{1f_y0u_Kn0w_En0uGH_y0u_Kn0w_1t_4ll}
