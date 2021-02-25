# Overview

Code from OSTEP chapter [Introduction](http://pages.cs.wisc.edu/~remzi/OSTEP/intro.pdf).

To compile, just type:
```
prompt> make
```

See the highly primitive `Makefile` for details.

Then, run them! Examples:

```
prompt> ./cpu A
```

```
prompt> ./mem 1
```
这个例子需要[关闭地址空间随机化(ASLR)](https://blog.csdn.net/white_eyes/article/details/7169199)

确认ASLR是否已经被打开，"2"表示已经打开

需要在root用户下，
echo 0 > /proc/sys/kernel/randomize_va_space 

```
prompt> ./threads 10000
```

```
prompt> ./io
```
为处理写入期间系统崩溃的问题，会引入一些保护机制和协议：如日志（journaling）或写时复制（copy-on-write）


## Details

One issue with mem.c is that address space randomization is usually on by
default. To turn it off:

### macOS
From [stackoverflow](http://stackoverflow.com/questions/23897963/documented-way-to-disable-aslr-on-os-x)

Just compile/link as follows:
    gcc -o mem mem.c -Wall -Wl,-no_pie

### Linux

From Giovanni Lagorio:

Under Linux you can disable ASLR, without using a debugger, in (at least)  two ways:
* Use the command setarch to run a process with ASLR disabled; I typically run
  bash, with which I can execute examples, like this:
  `setarch $(uname --machine) --addr-no-randomize /bin/bash`
* Writing 0 into `/proc/sys/kernel/randomize_va_space`; you need to be
  root to do this and this change has (a non-permanent) effect on the
  whole system, which is something you probably don't want. I use this
  one only inside VMs.



