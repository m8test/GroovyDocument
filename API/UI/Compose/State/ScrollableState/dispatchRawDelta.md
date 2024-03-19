功能:

+ 以像素为单位调度滚动增量，避免所有与滚动相关的机制。
  注意：与 [ScrollableState.scroll()](/API/UI/Compose/State/ScrollableState/README.md?id=scroll)
  不同，使用此方法调度任何增量都不会触发嵌套滚动，不会停止正在进行的滚动/拖动动画，并且会绕过任何优先级的滚动。此方法还将忽略 reverseDirection 和在 scrollable
  中设置的其他参数。该方法在内部用于嵌套滚动调度和其他低级操作，允许 [ScrollableState](/API/UI/Compose/State/ScrollableState/README.md) 的实现者根据自己的需要影响消耗。通过此方法手动调度增量可能会导致用户体验不佳，您必须首选
  [ScrollableState.scroll()](/API/UI/Compose/State/ScrollableState/README.md?id=scroll) 方法而不是此方法。

定义:

+ float dispatchRawDelta(float delta)

参数:

+ float delta - 嵌套滚动进程中分派的滚动量

返回值:

+ float - 消耗的增量

示例代码:

+ 启动一个Activity,
  并通过 [ScrollableState.dispatchRawDelta()](/API/UI/Compose/State/ScrollableState/README.md?id=dispatchRawDelta)
  方法以像素为单位调度滚动增量

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
                    // LazyListState.dispatchRawDelta() 用于以像素为单位调度滚动增量
                    lazyListState.dispatchRawDelta(100.0f)
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