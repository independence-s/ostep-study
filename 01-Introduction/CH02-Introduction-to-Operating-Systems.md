# CH02 - Introduction to Operating Systems

## 本章定位

这一章不是深入讲某个具体机制，而是在建立整本书的地图。

OSTEP 后面的主要内容围绕：

- Virtualization
- Concurrency
- Persistence

## The Crux

> How does the operating system virtualize resources?

重点不是只问“为什么要虚拟化”，而是继续追问：

- OS 用了什么 **mechanisms**？
- OS 使用什么 **policies**？
- 怎么保证足够 **efficient**？
- 需要什么 **hardware support**？

## 1. 操作系统是什么

可以先用一个直觉定义：

**操作系统是一整套帮助程序运行、管理资源并与硬件交互的系统软件。**

注意：

`a body of software` = 一整套软件 / 软件体系  
不是“软件的主体”。

## 2. Virtualizing the CPU

真实情况：

```text
少量物理 CPU
```

操作系统提供的效果：

```text
Program A → 好像有 CPU
Program B → 好像也有 CPU
Program C → 好像也有 CPU
```

这是一种 useful illusion（有用的假象/抽象）。

### 我的理解

虚拟化不是为了让“操作系统自己”更好用，而是为了：

> 让程序和用户更容易、安全、统一地使用有限且复杂的硬件资源。

## 3. Virtualizing Memory

程序看到的是自己的地址空间，而不是直接面对复杂的物理内存布局。

后续关键词：

- address space
- address translation
- paging
- TLB

## 4. Concurrency

多个执行流同时存在后，会出现：

- shared data
- race condition
- atomicity
- synchronization

后面会继续学习：

- thread
- lock
- condition variable
- semaphore

## 5. Persistence

数据不能只活在程序运行期间。

后面会学习：

- I/O
- disks
- files
- file systems
- crash consistency

## 6. Mechanism vs Policy

### Mechanism

回答：

> **怎么做到？**

例如：

- context switch
- trap
- interrupt
- page table

### Policy

回答：

> **有多个选择时选哪个？**

例如：

- 两个进程都想运行，先运行谁？
- 内存满了，淘汰哪个页面？

## 本章关键词

- operating system
- resource manager
- virtualization
- illusion
- mechanism
- policy
- hardware support
- API
- process identifier (PID)
- concurrency
- persistence

## 当前疑问

- [ ] library function 和 system call 的边界
- [ ] CPU virtualization 到底是怎么实现的
- [ ] API 如何进入 kernel
- [ ] process 和 program 的本质区别

## 一句话总结

**OSTEP 的导论是在建立一个问题框架：OS 如何通过机制、策略和硬件支持，把有限复杂的物理资源变成易用的抽象。**
