## 概述

[ScriptThread](/API/Thread/ScriptThread/README.md) 是脚本线程类,需要注意以下几点:

+ 一个脚本中只有一个主线程,但可以有多个子线程.
+ 主线程在运行脚本时会自动创建.
+ 创建新的线程可以通过 [Threads.startThread()](/API/Thread/Threads/README.md?id=startThread)
  方法实现,更多线程相关操作可参考 [Threads](/API/Thread/Threads/README.md)
+ 脚本主线程会等待所有子线程结束运行后再结束运行.
+ 如果脚本主线程异常结束,脚本中所有其他线程都会结束.
+ 脚本主线程结束标志着脚本停止运行.
+ 脚本线程结束需要同时满足以下条件:
    + 该脚本线程中的所有定时任务(参考 [Timer](/API/Thread/Timer/README.md))都执行完成
    + 该脚本线程没有启动任何后台服务(参考 [ScriptDaemon](/API/ScriptDaemon/README.md)),或者启动的后台服务已经停止运行.
    + 该脚本线程不在后台运行(
      [ScriptThread.background()](/API/Thread/ScriptThread/README.md?id=background))

## background()

[background](background.md ":include")

## interrupt()

[filename](interrupt.md ':include')

## isAlive()

[filename](isAlive.md ':include')

## isInterrupted()

[filename](isInterrupted.md ':include')

## isMainThread()

[isMainThread](isMainThread.md ":include")

## join()

[filename](join.md ':include')

## name()

[filename](name.md ':include')

## screenCapture()

[screenCapture](screenCapture.md ":include")

## timer()

[filename](timer.md ':include')
