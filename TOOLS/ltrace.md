# ltrace
# ltrace 常用指令
### ltrace [option ...] [command [arg ...]]

參數 | 說明
--- | ---
-a | 對齊具體某個列的返回值
-c | 計算時間和調用，並在程序退出時打印摘要
-C | 解碼低級別名稱（內核級）為用戶級名稱
-e | 改變跟踪的事件
-o | 把輸出定向到文件
-r | 輸出相對時間戳
-S | 顯示系統調用
-p PID | 附著在值為PID的進程號上進行ltrace
-s STRLEN | 設置輸出的字符串最大長度
-t、-tt、-ttt | 輸出絕對時間戳
-u USERNAME | 使用某個用戶id或組ID來運行命令


# 使用範例1

```
$ ltrace -c test
```
```
% time     seconds  usecs/call     calls      function
------ ----------- ----------- --------- --------------------
 20.13    0.000392          98         4 __freading
 19.31    0.000376         376         1 setlocale
 13.15    0.000256         128         2 fclose
 10.27    0.000200         100         2 fflush
  9.14    0.000178          89         2 __fpending
  8.53    0.000166          83         2 fileno
  5.96    0.000116         116         1 strrchr
  5.14    0.000100         100         1 bindtextdomain
  4.26    0.000083          83         1 textdomain
  4.11    0.000080          80         1 __cxa_atexit
------ ----------- ----------- --------- --------------------
100.00    0.001947                    17 total
```
#
```
$ ltrace -S test
```
```
SYS_brk(0)                                                                = 0x560202f0b000
SYS_access("/etc/ld.so.nohwcap", 00)                                      = -2
SYS_access("/etc/ld.so.preload", 04)                                      = -2
SYS_openat(0xffffff9c, 0x7f8fdfef0428, 0x80000, 0)                        = 3
SYS_fstat(3, 0x7ffe0ee60cc0)                                              = 0
SYS_mmap(0, 0x15a66, 1, 2)                                                = 0x7f8fe00e0000
SYS_close(3)                                                              = 0
SYS_access("/etc/ld.so.nohwcap", 00)                                      = -2
SYS_openat(0xffffff9c, 0x7f8fe00f8dd0, 0x80000, 0)                        = 3
SYS_read(3, "\177ELF\002\001\001\003", 832)                               = 832
SYS_fstat(3, 0x7ffe0ee60d20)                                              = 0
SYS_mmap(0, 8192, 3, 34)                                                  = 0x7f8fe00de000
SYS_mmap(0, 0x3f0ae0, 5, 2050)                                            = 0x7f8fdfade000
SYS_mprotect(0x7f8fdfcc5000, 2097152, 0)                                  = 0
SYS_mmap(0x7f8fdfec5000, 0x6000, 3, 2066)                                 = 0x7f8fdfec5000
SYS_mmap(0x7f8fdfecb000, 0x3ae0, 3, 50)                                   = 0x7f8fdfecb000
SYS_close(3)                                                              = 0
．．． ．．．
```
#
```
$ ltrace test
```
```
strrchr("test", '/')                                                      = nil
setlocale(LC_ALL, "")                                                     = "LC_CTYPE=en_US.UTF-8;LC_NUMERIC="...
bindtextdomain("coreutils", "/usr/share/locale")                          = "/usr/share/locale"
textdomain("coreutils")                                                   = "coreutils"
__cxa_atexit(0x55b7192bf530, 0, 0x55b7194c7008, 0x736c6974756572)         = 0
__fpending(0x7fa32222a760, 1, 0x55b7192bf530, 1)                          = 0
fileno(0x7fa32222a760)                                                    = 1
__freading(0x7fa32222a760, 1, 0x55b7192bf530, 1)                          = 0
__freading(0x7fa32222a760, 1, 4, 1)                                       = 0
fflush(0x7fa32222a760)                                                    = 0
fclose(0x7fa32222a760)                                                    = 0
__fpending(0x7fa32222a680, 0, 0x7fa322225760, 2880)                       = 0
fileno(0x7fa32222a680)                                                    = 2
__freading(0x7fa32222a680, 0, 0x7fa322225760, 2880)                       = 0
__freading(0x7fa32222a680, 0, 4, 2880)                                    = 0
fflush(0x7fa32222a680)                                                    = 0
fclose(0x7fa32222a680)                                                    = 0
+++ exited (status 1) +++
```
# 使用範例2
https://man.linuxde.net/ltrace
