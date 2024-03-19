功能:

+ 设置脚本名称,不能设置名称与其他正在运行的脚本名称相同,否则无法运行脚本

定义:

+ [ScriptStringConfig](/API/Script/ScriptStringConfig/README.md) name(String name)

参数:

+ String name - 脚本名称

返回值:

+ [ScriptStringConfig](/API/Script/ScriptStringConfig/README.md) - 返回对象本身方便链式调用

示例代码:

+ 通过 [ScriptStringConfig.name()](/API/Script/ScriptStringConfig/README.md?id=name) 方法设置脚本名称

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