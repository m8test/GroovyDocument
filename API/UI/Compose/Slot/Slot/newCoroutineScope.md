功能:

+ 创建 [CoroutineScope](/API/Coroutines/CoroutineScope/README.md) ,用于在协程中执行耗时操作,防止阻塞UI线程

定义:

+ [CoroutineScope](/API/Coroutines/CoroutineScope/README.md) newCoroutineScope(Closure closure)

参数:

+ Closure closure - 设置 [CoroutineContext](/API/Coroutines/CoroutineContext/README.md) 的闭包
    + 参数 - 无
    + delegate - [CoroutineContext](/API/Coroutines/CoroutineContext/README.md)

返回值:

+ [CoroutineScope](/API/Coroutines/CoroutineScope/README.md) -
  新创建的 [CoroutineScope](/API/Coroutines/CoroutineScope/README.md)

示例代码:

+ 启动一个Activity显示对话框,
  并通过 [Slot.newCoroutineScope()](/API/UI/Compose/Slot/Slot/README.md?id=newCoroutineScope)
  方法创建 [CoroutineScope](/API/Coroutines/CoroutineScope/README.md)

```groovy
def MyDialog = { state ->
    // delegate -> Slot
    // Slot.Dialog() 用于设置对话框
    Dialog {
        // delegate -> Dialog
        // Dialog.withSingleStates() 用于设置可组合项使用到的所有 SingleState
        withSingleStates(state)
        // Dialog.show() 用于显示对话框
        show(state.value())
        // Dialog.content() 用于设置对话框内容
        content {
            // delegate -> Slot
            // Slot.CircularProgressIndicator() 用于创建 CircularProgressIndicator 可组合项
            CircularProgressIndicator {
                // delegate -> CircularProgressIndicator
                // CircularProgressIndicator.color() 用于设置进度条颜色
                color {
                    // delegate -> Color
                    // Color.red() 用于配置红色通道
                    red(255)
                }
                // CircularProgressIndicator.strokeWidth() 用于设置进度条宽度
                strokeWidth(5)
            }
        }
    }
}

// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.mutableStateOf() 用于创建一个 MutableState 对象
    def state = mutableStateOf(false)
    // Slot.newCoroutineScope() 用于创建 CoroutineScope
    def coroutineScope = newCoroutineScope {
        // delegate -> CoroutineContext
    }
    MyDialog.delegate = delegate
    MyDialog(state)
    // Slot.Button() 用于创建 Button 可组合项
    Button {
        // delegate -> Button
        // Button.content() 用于设置按钮内容
        content {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("显示对话框")
            }
        }
        // Button.onClick() 用于处理点击事件
        onClick {
            state.value(true)
            // CoroutineScope.launch() 用于启动一个子协程(如果CoroutineContext设置了Job参数,那么就是启动一个新协程,与启动它的协程没有父子关系)
            coroutineScope.launch({
                // delegate -> CoroutineContext
                dispatcher("IO")
            }, "DEFAULT") {
                // delegate -> CoroutineScope
                // 模拟耗时操作
                // CoroutineScope.delay() 用于协程延时
                delay(4000)
                // CoroutineScope.withContext() 用于切换协程上下文
                withContext({
                    // delegate -> CoroutineContext
                    // CoroutineContext.dispatcher() 用于配置协程调度器
                    dispatcher("Main")
                }) {
                    // delegate -> CoroutineScope
                    // 隐藏对话框
                    state.value(false)
                }
            }
        }
    }
}
// Activity.onDestroy() 方法用于监听Activity销毁
$composeActivity.onDestroy {
    // Script.stop() 方法用于停止脚本
    $script.stop()
}
// Activity.start() 用于启动Android系统的Activity
$composeActivity.start()
```