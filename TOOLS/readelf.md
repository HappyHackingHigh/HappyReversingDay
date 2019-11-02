# readelf
# readelf 常用參數
```
參數 | 說明
--- | ---
-a | 顯示全部
-h | 顯示elf文件開始的文件頭
-l | 顯示程序頭表
-S | 顯示所有節頭信息
-r | 顯示可重定位段的
-d | 顯示動態節區的內容
-t | 顯示節詳細信息
-s | 顯示符號表
-p | <編號|名稱>將段<編號|名稱>的內容作為字符串轉儲
```

# 使用範例1
test.c
```
#include <stdio.h>

int x = 5;

int main()
{
   printf("Hello CTFer\n ”);
   return 0;
}
```
```
$ gcc -g test.c -o test
```

#
### 查看標頭檔
```
$ readelf -h test
```
```
ELF Header:
  Magic:   7f 45 4c 46 02 01 01 00 00 00 00 00 00 00 00 00 
  Class:                             ELF64
  Data:                              2's complement, little endian
  Version:                           1 (current)
  OS/ABI:                            UNIX - System V
  ABI Version:                       0
  Type:                              DYN (Shared object file)
  Machine:                           Advanced Micro Devices X86-64
  Version:                           0x1
  Entry point address:               0x540
  Start of program headers:          64 (bytes into file)
  Start of section headers:          8608 (bytes into file)
  Flags:                             0x0
  Size of this header:               64 (bytes)
  Size of program headers:           56 (bytes)
  Number of program headers:         9
  Size of section headers:           64 (bytes)
  Number of section headers:         34
  Section header string table index: 33
```
#
### 查看可執行文件的入口處
```
$ readelf -h test | grep Entry
```
```
Entry point address:               0x540
```
#
### 查看Sections header
```
$ readelf -S test
```
```
There are 34 section headers, starting at offset 0x21a0:

Section Headers:
  [Nr] Name              Type             Address           Offset
       Size              EntSize          Flags  Link  Info  Align
  [ 0]                   NULL             0000000000000000  00000000
       0000000000000000  0000000000000000           0     0     0
  [ 1] .interp           PROGBITS         0000000000000238  00000238
       000000000000001c  0000000000000000   A       0     0     1
  [ 2] .note.ABI-tag     NOTE             0000000000000254  00000254
       0000000000000020  0000000000000000   A       0     0     4
  [ 3] .note.gnu.build-i NOTE             0000000000000274  00000274
       0000000000000024  0000000000000000   A       0     0     4
  [ 4] .gnu.hash         GNU_HASH         0000000000000298  00000298
       000000000000001c  0000000000000000   A       5     0     8
  [ 5] .dynsym           DYNSYM           00000000000002b8  000002b8
       00000000000000a8  0000000000000018   A       6     1     8
  [ 6] .dynstr           STRTAB           0000000000000360  00000360
       0000000000000084  0000000000000000   A       0     0     1
```
# 使用範例2
https://ithelp.ithome.com.tw/articles/10193042
