# NASM
```
The Netwide Assembler, NASM, is an 80x86 and x86-64 assembler designed for portability and modularity.

https://zh.wikipedia.org/wiki/Netwide_Assembler
Netwide Assembler （簡稱 NASM）是一款基於英特爾 x86 架構的彙編與反彙編工具。
它可以用來編寫16位、32位（IA-32）和64位（x86-64）的程序。 
NASM被認為是Linux平台上最受歡迎的彙編工具之一

https://www.nasm.us/

下載:https://www.nasm.us/pub/nasm/releasebuilds/?C=M;O=D
```
# 使用nasm開發Windows 32位元組合程式(Assembly code)

# 使用nasm開發Windows 64位元組合程式(Assembly code)

# 使用nasm開發Linux Assembly Language
```
Assembly Language Step-by-Step: Programming With Linux, 3rd Edition
Duntemann, Jeff
John Wiley & Sons Inc
```

## NASM Tutorial
```
NASM Tutorial
https://cs.lmu.edu/~ray/notes/nasmtutorial/
```
### 在x86-64 linux使用nasm開發64位元組合程式(Assembly code)  hello.asm
```
; ----------------------------------------------------------------------------------------
; Writes "Hello, World" to the console using only system calls. Runs on 64-bit Linux only.
; To assemble and run:
;
;     nasm -felf64 hello.asm && ld hello.o && ./a.out
;
;https://cs.lmu.edu/~ray/notes/nasmtutorial/
; ----------------------------------------------------------------------------------------

          global    _start

          section   .text
_start:   mov       rax, 1                  ; system call for write
          mov       rdi, 1                  ; file handle 1 is stdout
          mov       rsi, message            ; address of string to output
          mov       rdx, 13                 ; number of bytes
          syscall                           ; invoke operating system to do the write
          mov       rax, 60                 ; system call for exit
          xor       rdi, rdi                ; exit code 0
          syscall                           ; invoke operating system to exit

          section   .data
message:  db        "Hello, World", 10      ; note the newline at the end
```
### 在x86-64 linux使用nasm開發64位元組合程式(Assembly code)  fib.asm
```
; -----------------------------------------------------------------------------
; A 64-bit Linux application that writes the first 90 Fibonacci numbers. To
; assemble and run:
;
;     nasm -felf64 fib.asm && gcc fib.o && ./a.out
; -----------------------------------------------------------------------------

        global  main
        extern  printf

        section .text
main:
        push    rbx                     ; we have to save this since we use it

        mov     ecx, 90                 ; ecx will countdown to 0
        xor     rax, rax                ; rax will hold the current number
        xor     rbx, rbx                ; rbx will hold the next number
        inc     rbx                     ; rbx is originally 1
print:
        ; We need to call printf, but we are using rax, rbx, and rcx.  printf
        ; may destroy rax and rcx so we will save these before the call and
        ; restore them afterwards.

        push    rax                     ; caller-save register
        push    rcx                     ; caller-save register

        mov     rdi, format             ; set 1st parameter (format)
        mov     rsi, rax                ; set 2nd parameter (current_number)
        xor     rax, rax                ; because printf is varargs

        ; Stack is already aligned because we pushed three 8 byte registers
        call    printf                  ; printf(format, current_number)

        pop     rcx                     ; restore caller-save register
        pop     rax                     ; restore caller-save register

        mov     rdx, rax                ; save the current number
        mov     rax, rbx                ; next number is now current
        add     rbx, rdx                ; get the new next number
        dec     ecx                     ; count down
        jnz     print                   ; if not done counting, do some more

        pop     rbx                     ; restore rbx before returning
        ret
format:
        db  "%20ld", 10, 0
```
#### Intro to x86 Assembly Language[32位元組合程式]
```
https://www.youtube.com/watch?v=wLXIWKUWpSs&list=PLmxT2pVYo5LB5EzTPZGfFN0c2GDiSXgQe
https://github.com/code-tutorials/assembly-intro
```
```
sudo apt-get install nasm
```
```
nasm -f elf32 example.asm -o example.o

ld -m elf_i386 example.o -o example

./example
```
```

```
#### NASM Assembly programming Tutorial
```
NASM Assembly programming Tutorial 01
https://www.youtube.com/watch?v=_JG4b7E_6-E

https://www.youtube.com/watch?v=hBhaaOwuocU

https://www.youtube.com/watch?v=4zfrjlTucLI

https://www.youtube.com/watch?v=faMLkpC8TmA
```

#### x86_64 Linux Assembly[64位元組合程式]
```
https://www.youtube.com/watch?v=VQAKkuLL31g&list=PLetF-YjXm-sCH6FrTz4AQhfH6INDQvQSn

x86_64 Linux Assembly #1 - "Hello, World!"
https://www.youtube.com/watch?v=VQAKkuLL31g



```
