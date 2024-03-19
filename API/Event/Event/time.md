功能:

+ 获取事件发布的时间

定义:

+ [ScriptDateTime](/API/DateTime/ScriptDateTime/README.md) time()

参数:

+ 无

返回值:

+ [ScriptDateTime](/API/DateTime/ScriptDateTime/README.md) - 事件发布的时间

示例代码:

+ 通过 [Event.time()](/API/Event/Event/README.md?id=time) 方法获取事件发布的时间

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Events.subscriber() 用于获取事件订阅器
def subscriber = $events.subscriber()
// Subscriber.subscribeLocal() 用于订阅本地事件
subscriber.subscribeLocal({
    // delegate -> LocalSubscription
    // LocalSubscription.channel() 用于设置本地订阅的频道
    channel("subscription channel")
    // LocalSubscription.id() 用于设置本地订阅的id
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
}
```