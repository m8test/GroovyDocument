功能:

+ 设置脚本是否需要在独立引擎中执行

定义:

+ [ScriptConfig](/API/Script/ScriptConfig/README.md) standalone(boolean standalone)

参数:

+ boolean standalone - 脚本启动参数

返回值:

+ [ScriptConfig](/API/Script/ScriptConfig/README.md) - 返回对象本身方便链式调用

示例代码:

+ 通过 [ScriptConfig.standalone()](/API/Script/ScriptConfig/README.md?id=standalone)
  方法设置脚本是否需要在独立引擎中执行

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// ScriptEngine.startScriptString() 用于启动脚本字符串
def script = $scriptEngine.startScriptString {
    // delegate -> ScriptStringConfig
    // ScriptStringConfig.content() 用于设置脚本内容
    content("\$console.log('来自字符串脚本')")
    // ScriptStringConfig.name() 用于设置脚本名称
    name("ScriptStringName")
    // ScriptStringConfig.language() 用于设置字符串脚本所属语言
    language("Groovy")
    // ScriptStringConfig.standalone() 用于设置脚本是否需要在独立引擎中执行
    standalone(true)
}
// Script.engine() 用于获取启动脚本的引擎
def engine = script.engine()
$assert.assertTrue($scriptEngine != engine, "脚本引擎不相同")
```