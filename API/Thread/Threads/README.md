## 概况

[Threads](/API/Thread/Threads/README.md) 是脚本线程管理类,可以对脚本中的线程进行管理,例如:

+ 线程睡眠
+ 获取主线程
+ 获取当前线程
+ 启动线程
+ 停止线程

TIPS:

+ 脚本主线程会等待所有子线程结束运行后再结束运行.
+ 如果脚本主线程异常结束,脚本中所有其他线程都会结束.
+ 脚本主线程结束标志着脚本停止运行.

## currentThread()

[currentThread](currentThread.md ':include')

## mainThread()

[mainThread](mainThread.md ':include')

## sleep()

[sleep](sleep.md ':include')

## startThread()

[startThread](startThread.md ':include')

## stopThread()

[stopThread](stopThread.md ':include')