---
layout: post
title:  "Reading"
categories: Linux
tags:  TheLinuxProgrammingInterface
author: LWL
---

* content
{:toc}
## 关于The Linux Programming Interface这本书的读书记录

### 前言

- 书封面还有一句话：A Linux & Unix System Programming Handbook
- 看书先看目录，应该是我从哪里学到的看书方法之一。关于这句话印象最深的就是在当年读高中的时候，了解到陈景润这个人，据说他在每天睡觉前会找一本书（或者是他在看一本新书前），先将目录仔细看一遍，然后通过目录自己去构想整本书的内容。强大如斯，自愧不如，能效仿的只有先看目录这么一个动作了。一千多页的书，其实光看目录再试图加以理解对于我来讲就要耗费好一段时间，不谈记住，有个大概的模糊的印象吧。
- 看这本书几个比较重要的点：锻炼加强英语阅读能力，Linux的深入理解

---

### 正文内容

- 第一大部分：History & Standards
  - 首先简单的介绍了Unix和C的历史
  - 其次简单的介绍了GNU项目以及Linux内核
  - 然后是Linux和C语言的标准化：标准化的目的是为了方便应用软件从一个系统到另一个系统的移植。介绍了SUSv3 and POSIX.1-2001等标准

- 第二大部分：fundamental concepts

  - 中心操作系统----内核：简单的介绍了内核的全貌，从内核怎样执行任务（进程安排，内存管理，文件系统的规定，创建终止进程，设备权限，网络，系统调用应用程序接口的规定），内核态用户态等

  - Shell：简单的说明了sh,ksh,csh,bash等

  - Users & Group:简单的介绍了用户以及群组的概念以及一些细节

  - 接下来简单的介绍了Linux的目录管理，文件类型，文件路径，文件权限等。

  - 文件I/O模式：系统调用：open(), read(), write(), close() 文件描述符：0,1,2分别代表stdin, stdout,stderr

  - programs:两种存在形式：human-readable such C、binary machine-language

  - process：可执行程序的实例。一个进程逻辑上分为以下几部分：

    - text 文本
    - data 程序使用的静态变量
    - heap 堆 程序分配的动态内存
    - stack 局部变量以及函数的存储区域

    ---

    fork()系统函数用来创建父进程，子进程是父进程的复制，同时继承了父进程的堆栈数据等的复制

    execue()系统函数用来执行进程，调用时会摧毁text，data，堆栈等

    ---

    进程ID的（PID）父进程ID（PPID）

    ---

    进程终止以及进程终止状态介绍

    ---

    每个进程都有用户以及用户组标识符：UIDS & GIDS同时分为真实的，有效的以及补充的。补充的只有GIDs。

    ---

    特权进程，init进程以及daemon(守护)进程的介绍

    ---

    环境列表：每个进程都有环境列表：记录着环境变量，主要是进程的用户空间内存。子进程同样进行对父进程的继承。

    






