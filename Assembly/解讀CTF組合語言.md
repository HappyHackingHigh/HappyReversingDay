
#
```


```

## pico-ctf-2014 reverse-engineering/basic-asm-60

### 題目
```
pico-ctf-2014 reverse-engineering/basic-asm-60

We found this program snippet.txt, but we're having some trouble figuring it out. 
What's the value of %eax when the last instruction (the NOP) runs?
```
snippet.txt
```
# This file is in AT&T syntax - see http://www.imada.sdu.dk/Courses/DM18/Litteratur/IntelnATT.htm
# and http://en.wikipedia.org/wiki/X86_assembly_language#Syntax. Both gdb and objdump produce
# AT&T syntax by default.
MOV $10814,%ebx
MOV $2972,%eax
MOV $10017,%ecx
CMP %eax,%ebx
JL L1
JMP L2
L1:
IMUL %eax,%ebx
ADD %eax,%ebx
MOV %ebx,%eax
SUB %ecx,%eax
JMP L3
L2:
IMUL %eax,%ebx
SUB %eax,%ebx
MOV %ebx,%eax
ADD %ecx,%eax
L3:
NOP
```

### 解答

#### 分析

```
x86系列處理器從其第一代產品英特爾8086開始就提供了一條專門用來支援調試的指令，即INT 3。
指令的目的就是使CPU中斷（break）到調試器，以供調試者對執行現場進行各種分析。
當我們偵錯工具時，可以在可能有問題的地方插入一條INT 3指令，使CPU執行到這一點時停下來。
這便是軟體調試中經常用到的中斷點（breakpoint）功能，因此INT 3指令又被稱為中斷點指令。
```
將原本給的程式加上關鍵中斷===> 程式名稱設為basic.s
```
.global main
.text
main:

MOV $10814,%ebx
MOV $2972,%eax
MOV $10017,%ecx
CMP %eax,%ebx
JL L1
JMP L2
L1:
IMUL %eax,%ebx
ADD %eax,%ebx
MOV %ebx,%eax
SUB %ecx,%eax
JMP L3
L2:
IMUL %eax,%ebx
SUB %eax,%ebx
MOV %ebx,%eax
ADD %ecx,%eax
L3:
INT3
NOP
```

步驟二:
```
gcc -o basic basic.s
```
```
gdb ./basic -q -batch -n -ex 'r' -ex 'p $eax'
```
就可以看到結果
```
Program received signal SIGTRAP, Trace/breakpoint trap.
0x8000058a in L3 ()
$1 = XXXXXXXXXX(這個數字就是答案)
```
