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
#### Intro to x86 Assembly Language[32位元組合程式]
```
https://www.youtube.com/watch?v=wLXIWKUWpSs&list=PLmxT2pVYo5LB5EzTPZGfFN0c2GDiSXgQe
```
```
sudo apt-get install nasm
```
```
nasm -f elf32 example.asm -o example.o

ls -m elf_i386 example.o -o example

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
