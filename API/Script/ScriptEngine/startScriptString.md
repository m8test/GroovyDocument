功能:

+ 启动脚本字符串

定义:

+ [Script](/API/Script/Script/README.md) startScriptString(Closure closure)

参数:

+ Closure closure - 设置脚本配置的闭包
    + 参数 - 无
    + delegate - [ScriptStringConfig](/API/Script/ScriptStringConfig/README.md)

返回值:

+ [Script](/API/Script/Script/README.md) - 返回启动的脚本对象,如果启动脚本失败则返回null

示例代码:

+ 通过 [ScriptEngine.startScriptString()](/API/Script/ScriptEngine/README.md?id=startScriptString)
  方法启动脚本字符串

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// ScriptEngine.startScriptString() 用于启动脚本字符串
$scriptEngine.startScriptString {
    // delegate -> ScriptStringConfig
    // ScriptStringConfig.content() 用于设置脚本内容
    content("\$console.log('来自字符串脚本')")
    // ScriptStringConfig.name() 用于设置脚本名称
    name("ScriptStringName")
    // ScriptStringConfig.language() 用于设置字符串脚本所属语言
    language("Groovy")
}
```