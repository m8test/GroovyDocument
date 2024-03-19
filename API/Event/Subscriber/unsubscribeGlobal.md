功能:

+ 取消订阅全局事件

定义:

+ boolean unsubscribeGlobal(String subscriptionId)

参数:

+ String subscriptionId - 全局订阅的id

返回值:

+ boolean - 取消订阅成功返回true,失败返回false

示例代码:

+ 通过 [Subscriber.unsubscribeGlobal()](/API/Event/Subscriber/README.md?id=unsubscribeGlobal)
  方法取消订阅全局事件

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Events.subscriber() 用于获取事件订阅器
def subscriber = $events.subscriber()
// Subscriber.subscribeGlobal() 用于订阅全局事件
subscriber.subscribeGlobal({
    // delegate -> GlobalSubscription
    // GlobalSubscription.channel() 用于设置全局订阅的频道
    channel("subscription channel")
    // GlobalSubscription.id() 用于设置全局订阅的id
    id("subscription id")
}) {
    // it -> Event
    // Event.channel() 用于获取事件发布的频道
    $assert.assertTrue(it.channel() == "subscription channel", "事件频道")
    // Event.data() 用于获取事件中包含的数据
    $assert.assertTrue(it.data() == "data from event", "事件数据")
    // Event.time() 用于获取事件发布的时间
    $console.log("事件发布时间->" + it.time())
}
// Subscriber.unsubscribeGlobal() 用于取消订阅全局事件
$assert.assertTrue(subscriber.unsubscribeGlobal("subscription id"), "取消全局订阅")
// ScriptEngine.startScriptFile() 用于启动脚本文件
$scriptEngine.startScriptFile {
    // delegate -> ScriptFileConfig
    // Files.buildFile() 用于构建一个 ScriptFile 对象
    def scriptFile = $files.buildFile {
        // delegate -> FileBuilder
        // FileBuilder.res() 用于配置文件路径为项目资源文件路径
        res("scriptFile.groovy")
    }
    // ScriptFileConfig.file() 用于设置脚本文件路径
    file(scriptFile)
    // ScriptFileConfig.standalone() 用于设置脚本是否需要在独立引擎中执行
    standalone(true)
}
// Threads.mainThread() 用于获取脚本主线程
def mainThread = $threads.mainThread()
// ScriptThread.timer() 用于获取线程对应的定时器
def timer = mainThread.timer()
// Timer.setTimeout() 用于添加一个延时执行的定时任务
timer.setTimeout({
    // 保持脚本3秒钟不结束
}, 3000)
```