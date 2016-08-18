# RabbitOS

**参考书目：一个操作系统的实现**

##章节

###第一章

wow 好酷！

###第二章

配环境。
配环境。
配环境。

一定要装**32位**的Ubuntu ！！！
64位的系统从书上P140开始遇到的**ld**指令和32位系统**不兼容**，并且没有很好的办法模拟32位操作。

bochs进入调试模式要按c 开始模拟！

###第三章

懵逼。

###第四章

boot.bin **->** loader.bin

从boot引导扇区启动,然后加载loader

###第五章

**用汇编语言写hello world！**

boot.bin <b style="color:red;">-></b> loader.bin <b style="color:red;">-></b> kernel.bin

实现了从引导扇区的启动,加载loader,再从loader加载kernel,进入保护模式。

增加了异常处理机制。

**接下来的工作是在已经搭建好的框架上完成，并且大部分将用可读性较好的C语言编写**

**"最困难的日子已经过去，虽然眼前的路仍然很长，但是我们不再感觉是在无边的黑暗中探索，眼前是一条光明大道，等待我们踏入新的征程。"**

###第六章

进程！！！

完成进程调度 需要

1.时钟中断处理程序
2.进程调度模块
3.多个进程体

时钟中断是用汇编写的-_-! (就不说了

进程调度也是在中断中处理的 (也是汇编

---------------准备进程表---------------

测试用的进程只是一个无限循环打印字母A和i++的函数，但是实现从ring0到ring1的跳转并执行这个进程需要很多步骤，特别是对堆栈段的处理，TSS|GDT|LDT|SS...
PCB进程控制块是一个是s_proc的结构体,该结构体的第一个成员还是一个结构体(s_stackframe)，存储所有的寄存器的值。

中断处理
解决嵌套重入中断问题，添加一个全局变量k_reenter = -1; 每进入一次嵌套中断自增，判断是否为0来知道是否嵌套中断。

学习借鉴Minix的中断处理模块后修改了本来的代码，将其模块化 划分成save | restart 等多段清晰的代码段。
算是达到了一个里程碑 (黑人问号？？？？

接下来谈到了系！统！调！用！

终于在第247页讲到了我一直很想知道的时钟中断的时间间隔以及由谁产生的中断！

**进程调度**

在之前实现的时间片轮转调度算法后，再实现了简单的优先级调度～


###第七章

I/O！！！

P267 & P268 ----- 键盘中断 MakeCode & BreakCode

各种与运算或与运算宝宝看不懂啊！！！！
什么鬼啊！！！

#####垃圾Bug - 0
垃圾GCC编译器版本 makefile不通过

Error : undefined reference to `__stack_chk_fail'

需要改MakeFile里面的CFLAGS 加上**-fno-stack-protector**
CFLAGS	= -I include/ -c -fno-builtin -fno-stack-protector

#####垃圾Bug - 1
在bochs下按Alt + Fn 这个组合键只会相应ubuntu的全局快捷键，不能响应虚拟机里面的操作 **冷漠**
于是请教吕老师，给出的回答是把Alt + Fn组合键改成ctrl + Fn这种组合键 **简单粗暴**

P315 ----- 增加一个系统调用 需要的步骤。


###第八章

进程间通信！！！

Minix->微内核<br>Linux->宏内核

assert() 和 panic() 

printl() --> printf() --> printx()

将之前的get_ticks()用消息通信机制重新实现，内核态代码大概不会再改动～


###第九章

文件系统！！！

硬盘驱动程序 硬盘系统进程

用bximage新建一个80M的硬盘 '80m.img'

SuperBlock -> Metadata
Sector map
inode_array
inode map

分区好复杂？？？


<br><br>

>希望每天都能commit

continue...
