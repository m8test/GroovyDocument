## 概述

定时器可以实现定时执行任务,需要注意以下几点:

+ 每个脚本线程都有并且只有一个定时器,可以通过 [ScriptThread.timer()](/API/Thread/ScriptThread/README.md?id=timer)
  获取脚本线程对应的定时器.
+ 添加定时任务可以通过以下方法实现:
    + [Timer.setTimeout()](/API/Thread/Timer/README.md?id=setTimeout): 添加延时执行的定时任务
    + [Timer.setImmediate()](/API/Thread/Timer/README.md?id=setImmediate): 添加立即执行的定时任务
    + [Timer.setInterval()](/API/Thread/Timer/README.md?id=setInterval): 添加无限循环执行的定时任务
+ 取消定时任务可通过以下方法实现:
    + [Timer.clearTimeout()](/API/Thread/Timer/README.md?id=clearTimeout): 添加延时执行的定时任务
    + [Timer.clearImmediate()](/API/Thread/Timer/README.md?id=clearImmediate): 添加立即执行的定时任务
    + [Timer.claarInterval()](/API/Thread/Timer/README.md?id=clearInterval): 添加无限循环执行的定时任务
+ 同一个定时器(Timer)添加的定时任务会按照时间顺序排序,然后一个一个执行,在前一个定时任务执行完成之前,后一个定时任务无法执行.
  例如尽管 [Timer.setImmediate()](/API/Thread/Timer/README.md?id=setImmediate)
  是立即执行的定时任务,但是不代表它会立即执行,而是会添加到定时任务队列中排序,只有等排在它前面的所有定时任务都执行完之后才能执行.
+ 同一个定时器(Timer)添加的定时任务都会在同一线程同步执行.
+ 用户代码本身可以看所是一个立即执行的定时任务,运行在脚本主线程,所以在脚本主线程添加的定时任务在用户代码执行完之前,所有在脚本主线程的定时任务都无法执行.
+ 定时任务定时的时间不一定会准确,因为有可能前一个定时任务执行的时间本身就超过了后一个定时任务的延时时间.
+ 如果某个脚本线程(定时器)中的定时任务中写了死循环,那么这个定时任务就不会执行完成,所有在这个脚本线程中位于此定时任务后面的定时任务都无法得到执行.但是其他线程中的定时任务不会受到影响.
+ 定时任务执行完成的条件:
    + 对于 [Timer.setTimeout()](/API/Thread/Timer/README.md?id=setTimeout)
      和 [Timer.setImmediate()](/API/Thread/Timer/README.md?id=setImmediate)
      添加的定时任务,只要closure里面的代码执行完或者通过对应的取消定时任务的方法 [Timer.clearTimeout()](/API/Thread/Timer/README.md?id=clearTimeout)
      和 [Timer.clearImmediate()](/API/Thread/Timer/README.md?id=clearImmediate)
      取消该定时任务都表示该定时任务已经表示该定时任务已经完成.
    + 对于 [Timer.setInterval()](/API/Thread/Timer/README.md?id=setInterval)
      ,只有通过 [Timer.claarInterval()](/API/Thread/Timer/README.md?id=clearInterval) 取消该定时任务才算完成.
      也就是说如果一个ScriptThread设置了Interval定时任务没有被取消,那么正常情况下这个线程永远都不会停止.当然除了异常情况,例如抛异常,手动停止脚本运行等.

## clearImmediate()

[filename](clearImmediate.md ':include')

## clearInterval()

[filename](clearInterval.md ':include')

## clearTimeout()

[filename](clearTimeout.md ':include')

## setImmediate()

[filename](setImmediate.md ':include')

## setInterval()

[filename](setInterval.md ':include')

## setTimeout()

[filename](setTimeout.md ':include')
