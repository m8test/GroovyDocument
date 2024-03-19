## 概述

控制台主要接收来自脚本的输出日志,输出信息到控制台的方法如下:

+ [Console.log()](/API/Console/Console/README.md?id=log)
+ [Console.verbose()](/API/Console/Console/README.md?id=verbose)
+ [Console.info()](/API/Console/Console/README.md?id=info)
+ [Console.warn()](/API/Console/Console/README.md?id=warn)
+ [Console.error()](/API/Console/Console/README.md?id=error)
+ [Console.assert()](/API/Console/Console/README.md?id=assert)

除了[输出日志](/Console/README.md?id=输出信息)之外,控制台还可以实现[计数](/Console/README.md?id=计数)
,[计时](/Console/README.md?id=计时)等功能.

## 输出日志

[Console](/API/Console/Console/README.md) 类提供了输出多种类型的信息功能,没有本质上的区别,用法也类似,实例代码如下:

[filename](output.md ':include')

## 计时

计时功能需要结合 [Console.time()](/API/Console/Console/README.md?id=time)
和 [Console.timeEnd()](/API/Console/Console/README.md?id=timeEnd) 方法实现,实例代码如下:

[filename](time_timeEnd.md ':include')

## 计数

计数可以通过 [Console.count()](/API/Console/Console/README.md?id=count) 方法实现,每次调用都会加1,可以将一个字符串(计数器标识)
作为参数传递到方法中设置不同的计数器.

[filename](count.md ':include')

计数器也可以重置,通过 [Console.countReset()](/API/Console/Console/README.md?id=countReset)
方法实现,参数为一个字符串,也就是计数器的标识.

[filename](countReset.md ':include')

## 清空日志

如果觉得日志信息太多了,可以通过 [Console.clear()](/API/Console/Console/README.md?id=clear) 方法将控制台之前所有的信息清空.

[filename](clear.md ':include')

## 设置/获取日志容量

默认情况下控制台不限制日志数量大小,可以无限输出,但是如果想要指定日志容量的话,可以通过 [Console.size()](/API/Console/Console/README.md?id=size)
方法设置.

[filename](size.md ':include')
