功能:

+ 设置脚本启动参数

定义:

+ [ScriptConfig](/API/Script/ScriptConfig/README.md) arguments(List\<String\> arguments)

参数:

+ List\<String\> arguments - 脚本启动参数

返回值:

+ [ScriptConfig](/API/Script/ScriptConfig/README.md) - 返回对象本身方便链式调用

示例代码:

+ 通过 [ScriptConfig.arguments()](/API/Script/ScriptConfig/README.md?id=arguments) 方法设置脚本启动参数

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// ScriptEngine.startScriptString() 用于启动脚本字符串
$scriptEngine.startScriptString {
    // delegate -> ScriptStringConfig
    // ScriptStringConfig.content() 用于设置脚本内容
    content("\$console.log(\$arguments[0], \$arguments[1], \$arguments[2])")
    // ScriptStringConfig.name() 用于设置脚本名称
    name("ScriptStringName")
    // ScriptStringConfig.language() 用于设置字符串脚本所属语言
    language("Groovy")
    // ScriptStringConfig.arguments() 用于设置脚本启动参数
    arguments(["argument1", "argument2", "argument3"])
}
```