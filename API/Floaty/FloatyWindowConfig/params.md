功能1:

+ 设置悬浮窗布局参数(
  [LayoutParams](https://developer.android.google.cn/reference/android/view/WindowManager.LayoutParams) )

定义1:

+ [FloatyWindowConfig](/API/Floaty/FloatyWindowConfig/README.md) params(Closure config)

参数1:

+ Closure config - 配置悬浮窗口布局参数的闭包
    + 参数 - 无
    + delegate - [LayoutParams](
      https://developer.android.google.cn/reference/android/view/WindowManager.LayoutParams)

返回值1:

+ [FloatyWindowConfig](/API/Floaty/FloatyWindowConfig/README.md) - 返回对象本身方便链式调用

功能2:

+ 获取悬浮窗布局参数(
  [LayoutParams](https://developer.android.google.cn/reference/android/view/WindowManager.LayoutParams) )

定义2:

+ [LayoutParams](https://developer.android.google.cn/reference/android/view/WindowManager.LayoutParams)
  params()

参数2:

+ 无

返回值2:

+ [LayoutParams](
  https://developer.android.google.cn/reference/android/view/WindowManager.LayoutParams) -
  当前悬浮窗布局参数对象

示例代码:

+ 显示一个悬浮窗口并通过 [FloatyWindowConfig.params()](/API/Floaty/FloatyWindowConfig/README.md?id=params)
  方法设置/获取悬浮窗布局参数([LayoutParams](https://developer.android.google.cn/reference/android/view/WindowManager.LayoutParams))

```groovy
def MyButton = { floatyWindow, buttonText, buttonOnClick ->
    // delegate -> Slot
    // Slot.Button() 用于创建 Button 可组合项
    Button {
        // delegate-> Button
        // Button.content() 用于设置 Button 可组合项中的内容
        content {
            // delegate -> Slot
            // Slot.Text() 用于创建 Text 可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置 Text 可组合项的文本内容
                text(buttonText)
            }
        }
        // Button.onClick() 用于处理 Button 可组合项的点击事件
        onClick {
            buttonOnClick()
        }
    }
}

// Floaty.window() 用于显示一个悬浮窗口
def window = $floaty.window({
    // delegate -> FloatyWindowConfig
    // FloatyWindowConfig.title() 用于配置悬浮窗口的标题
    title("这是标题")
    // FloatyWindowConfig.params() 用于设置悬浮窗布局参数(LayoutParams)
    params {
        // delegate -> LayoutParams
        x = 100
    }
}) { floatyWindow ->
    // delegate -> Slot
    // Slot.Surface() 用于创建Surface可组合项
    Surface {
        // delegate -> Surface
        // Composable.modifier() 用于修饰 Composable,Surface 继承自 Composable
        modifier {
            // delegate -> Modifier
            // Modifier.fillMaxSize() 用于设置填充父可组合项宽度和高度, 参数为填充父可组合项的比例, 取值区间为 0.0f-1.0f
            fillMaxSize(1.0f)
        }
        // Surface.content() 用于设置 Surface 可组合项的内容
        content {
            // delegate -> Slot
            // Slot.Column() 用于创建 Column 可组合项
            Column {
                // delegate -> Column
                // Column.content() 用于设置 Column 可组合项中的内容
                content {
                    // delegate -> Slot
                    MyButton.delegate = delegate
                    MyButton(floatyWindow, "透明度+0.1") {
                        // FloatWindow.config() 用于更新悬浮窗配置
                        floatyWindow.config {
                            // delegate -> FloatyWindowConfig
                            // FloatyWindowConfig.params() 用于获取悬浮窗布局参数(LayoutParams)
                            def layoutParams = params()
                            def alphaResult = layoutParams.alpha + 0.1f
                            if (alphaResult <= 1.0f) {
                                layoutParams.alpha = alphaResult
                            }
                        }
                    }
                    MyButton(floatyWindow, "透明度-0.1") {
                        // FloatWindow.config() 用于更新悬浮窗配置
                        floatyWindow.config {
                            // delegate -> FloatyWindowConfig
                            // FloatyWindowConfig.params() 用于获取悬浮窗布局参数(LayoutParams)
                            def layoutParams = params()
                            def alphaResult = layoutParams.alpha - 0.1f
                            if (alphaResult >= 0.0f) {
                                layoutParams.alpha = alphaResult
                            }
                        }
                    }
                }
            }
        }
    }
}
def config = window.config()
// FloatyWindowConfig.title() 用于获取悬浮窗标题
$assert.assertTrue(config.title() == "这是标题", "悬浮窗标题")
```