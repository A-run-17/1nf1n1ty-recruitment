# Favourite byte
For the next few challenges, you'll use what you've just learned to solve some more XOR puzzles.

I've hidden some data using XOR with a single byte, but that byte is a secret. Don't forget to decode from hex first.

       73626960647f6b206821204f21254f7d694f7624662065622127234f726927756d

# Python Script
```
from pwnlib.util.fiddling import xor

data = bytes.fromhex("73626960647f6b206821204f21254f7d694f7624662065622127234f726927756d")

for key in range(256):
    result = xor(data,key)
    if b"crypto" in result:
        print("Key =",key," Flag =", result.decode('ascii'))
```

# Solution
The key is not given so using brute forcing attack we can find the key and obtain the flag for this level

     Flag  :  crypto{0x10_15_my_f4v0ur173_by7e}
