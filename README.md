# OSTEP 学习仓库

这套目录用于学习 *Operating Systems: Three Easy Pieces (OSTEP)*。

核心原则：不要把这里变成原文摘抄仓库，而要围绕 **问题 → 抽象 → 机制 → 策略 → 代码 → 实验 → 易错点** 建立自己的操作系统知识体系。

## 三条主线

1. **Virtualization（虚拟化）**
   - CPU → Process / Scheduling
   - Memory → Address Space / Paging / TLB
2. **Concurrency（并发）**
   - Threads / Locks / Condition Variables / Semaphores / Bugs
3. **Persistence（持久化）**
   - I/O / Disks / Files / File Systems / Crash Consistency

## 推荐学习流程

每学一章：

1. 先找到本章的 **The Crux of the Problem**
2. 用一句话说出“这一章到底解决什么问题”
3. 找出 OS 提供的抽象
4. 区分 **Mechanism（机制）** 与 **Policy（策略）**
5. 画出执行时间线或数据流
6. 跑书里的代码或 simulator
7. 完成 homework
8. 最后再整理笔记，而不是一边读一边机械抄写

## 文件命名

推荐：

`CHxx-英文标题.md`

例如：

- `CH02-Introduction-to-Operating-Systems.md`
- `CH04-The-Abstraction-Process.md`
- `CH28-Locks.md`

## 原文怎么处理

建议继续使用 OSTEP 官方网页/PDF 作为原文来源。
这里仅保存：
- 关键短句
- 术语
- 你的理解
- 图解
- 代码实验
- 作业记录

这样仓库会越来越像“你自己的操作系统教材”。
