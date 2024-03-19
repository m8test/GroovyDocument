## 概述

M8Test提供多线程支持,每个脚本都可以启动多个线程来执行任务,需要注意以下方面:

+ 每个脚本都会有一个主线程,在脚本运行时自动创建.
+ 脚本主线程会等待此脚本中的其他线程执行完成才会停止.
+ 如果主线程意外停止,例如抛异常,那么其他子线程也会随着主线程的停止而停止.
+ 主脚本停止运行代表着脚本已经执行结束.
+ 一个线程结束需要同时满足以下两个条件:
    + 该脚本线程中的所有定时任务(参考 [Timer](/API/Thread/Timer/README.md))都执行完成
    + 该脚本线程没有启动任何后台服务(参考 [Service](/API/Service/README.md)),或者启动的后台服务已经停止运行.

## 启动新线程

启动一个线程非常简单,只需要调用 [Threads.startThread()](/API/Thread/Threads/README.md?id=startThread)
方法即可.

[filename](startThread.md ':include')

[Threads.startThread()](/API/Thread/Threads/README.md?id=startThread)
方法会返回一个 [ScriptThread](/API/Thread/ScriptThread/README.md) 对象,可以通过此对象对线程进行管理.

## 停止线程

停止线程的方式有两种,一种是[暴力停止](/Thread/README.md?id=暴力停止),一种是[非暴力停止](/Thread/README.md?id=非暴力停止).

### 暴力停止

+ 所谓的暴力停止指的是无论线程执行状态是什么,都将其停止.
+ 例如,线程正在下载一个文件,如果通过此方式停止线程,那么无论文件有没有下载完,该线程都会被停止.
+ 暴力停止线程可通过 [Threads.stopThread()](/API/Thread/Threads/README.md?id=stopThread)
  方法实现,此方法参数为 [ScriptThread](/API/Thread/ScriptThread/README.md)
  对象,也就是 [Threads.startThread()](/API/Thread/Threads/README.md?id=startThread) 的返回值.
+ 如果想停止主线程可以通过 [Threads.mainThread()](/API/Thread/Threads/README.md?id=mainThread)
  获取主线程对象,然后再将其作为参数传给 [Threads.stopThread()](/API/Thread/Threads/README.md?id=stopThread)
  方法即可.

[filename](stopThread.md ':include')

### 非暴力停止

所谓的非暴力停止指的是线程中断机制( [ScriptThread.interrupt()](/API/Thread/ScriptThread/README.md?id=interrupt)
和 [ScriptThread.isInterrupted()](/API/Thread/ScriptThread/README.md?id=isInterrupted) 配合使用)
,可以实现等到文件下载成功后再停止线程,停止线程方法如下:

+ 首先需要调用 [ScriptThread.interrupt()](/API/Thread/ScriptThread/README.md?id=interrupt)
  方法将线程设置为中断状态,但此时线程不会停止仍然会运行.

+ 其次需要调用 [ScriptThread.isInterrupted()](/API/Thread/ScriptThread/README.md?id=isInterrupted)
  方法获取中断状态,当线程处于中断状态就执行线程停止操作(例如写个死循环,每次循环检测中断状态,如果线程中断了就跳出死循环).

[filename](stopThreadManually.md ':include')

## 定时任务

定时任务可以通过定时器( [Timer](/API/Thread/Timer/README.md) )
添加,每个线程( [ScriptThread](/API/Thread/ScriptThread/README.md) )
都会有一个定时器并且只有一个定时器,可以通过调用 [ScriptThread.timer()](/API/Thread/ScriptThread/README.md?id=timer)
获取线程对应的定时器,定时器可以添加的定时任务有:

+ 立即执行任务
+ 延时执行任务
+ 无限循环执行任务

### 立即执行任务

立即执行任务可以通过调用 [Timer.setImmediate()](/API/Thread/Timer/README.md?id=setImmediate) 方法添加

[filename](setImmediate.md ':include')

### 延时执行任务

延时执行任务可以通过调用 [Timer.setTimeout()](/API/Thread/Timer/README.md?id=setTimeout) 方法添加

[filename](setTimeout.md ':include')

### 无限循环执行任务

无限循环执行任务可以通过调用 [Timer.setInterval()](/API/Thread/Timer/README.md?id=setInterval) 方法添加

[filename](setInterval.md ':include')

