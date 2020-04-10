---
post: page
title: GCD与NSOperationQueue使用时机
tags: [iOS,GCD,NSOperationQueue]
comment: true
---


## 何时使用Grand Central Dispatch
调度队列，组，信号量，源和屏障包括一组基本的并发原语，并在其上构建了所​​有系统框架。

对于一次性计算或只是简单地加快现有方法的速度，使用轻量级GCD调度通常比使用NSOperation更为方便。

## 何时使用NSOperation
NSOperation可以按照一组特定队列优先级和服务质量的依赖项进行调度。与在GCD队列上安排的块不同，可以取消NSOperation并查询其操作状态。通过子类化，NSOperation可以将其工作结果与自身关联起来，以备将来参考。

只需记住：NSOperation和Grand Central Dispatch并不互斥。创造性和有效地使用两者是开发强大而高性能的iOS或OS X应用程序的关键。
