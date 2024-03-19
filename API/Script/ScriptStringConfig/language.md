功能:

+ 设置字符串脚本所属语言

定义:

+ [ScriptStringConfig](/API/Script/ScriptStringConfig/README.md) language(String language)

参数:

+ String language - 字符串脚本所属语言

返回值:

+ [ScriptStringConfig](/API/Script/ScriptStringConfig/README.md) - 返回对象本身方便链式调用

示例代码:

+ 通过 [ScriptStringConfig.language()](/API/Script/ScriptStringConfig/README.md?id=language)
  方法设置字符串脚本所属语言

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