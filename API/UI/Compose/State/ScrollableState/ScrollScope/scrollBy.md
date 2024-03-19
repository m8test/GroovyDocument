功能:

+ 尝试按像素px向前滚动。

定义:

+ float scrollBy(Number pixel)

参数:

+ Number pixel - 滚动的像素大小

返回值:

+ float - 消耗的请求滚动量（即滚动的距离）

示例代码:

+ 启动一个Activity,
  并通过 [ScrollScope.scrollBy()](/API/UI/Compose/State/ScrollableState/ScrollScope/README.md?id=scrollBy)
  方法尝试按像素px向前滚动。

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.newLazyListState() 用于创建 LazyListState
    def lazyListState = newLazyListState {
        // delegate -> LazyListState
    }
    // Slot.Row() 用于创建 Row 可组合项
    Row {
        // delegate -> Row
        // Row.content() 用于设置行内容
        content {
            // delegate -> Slot
            // Slot.LazyColumn() 用于创建 LazyColumn 可组合项
            LazyColumn {
                // delegate -> LazyColumn
                // LazyList.state() 用于设置 LazyListState
                state(lazyListState)
                // LazyList.content() 用于设置列表内容
                content {
                    // delegate -> LazyListScope
                    // LazyListScope.items() 用于添加多个项目到列表中
                    items(100) { index, value ->
                        // delegate -> Slot
                        // Slot.Text() 用于创建文本可组合项
                        Text {
                            // delegate -> Text
                            // Text.modifier() 用于修饰 Composable
                            modifier {
                                // delegate -> Modifier
                                // Modifier.height() 用于设置高度
                                height(250)
                            }
                            // Text.text() 用于设置文本可组合项内容
                            text("item$index")
                        }
                    }
                }
            }
            // Slot.Button() 用于创建 Button 可组合项
            Button {
                // delegate -> Button
                // Button.content() 用于设置按钮内容
                content {
                    // delegate -> Slot
                    // Slot.Text() 用于创建文本可组合项
                    Text {
                        // delegate -> Text
                        text("滑动")
                    }
                }
                // Button.onClick() 用于处理点击事件
                onClick {
                    // LazyListState.scroll() 用于滚动懒列表
                    lazyListState.scroll("PreventUserInput") {
                        // delegate - ScrollScope
                        // ScrollScope.scrollBy() 用于尝试按像素px向前滚动。
                        scrollBy(100)
                    }
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