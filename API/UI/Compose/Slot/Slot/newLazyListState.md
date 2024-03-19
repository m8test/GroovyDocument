功能:

+ 创建 [LazyListState](/API/UI/Compose/State/LazyListState/README.md)

定义:

+ [LazyListState](/API/UI/Compose/State/LazyListState/README.md) newLazyListState(Closure closure)

参数:

+ Closure closure - 设置 [LazyListState](/API/UI/Compose/State/LazyListState/README.md) 的闭包
    + 参数 - 无
    + delegate - [LazyListState](/API/UI/Compose/State/LazyListState/README.md)

返回值:

+ [LazyListState](/API/UI/Compose/State/LazyListState/README.md) -
  新创建的 [LazyListState](/API/UI/Compose/State/LazyListState/README.md)

示例代码:

+ 启动一个Activity, 并通过 [Slot.newLazyListState()](/API/UI/Compose/Slot/Slot/README.md?id=newLazyListState)
  方法创建 [LazyListState](/API/UI/Compose/State/LazyListState/README.md)

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
                        // Text.text() 用于设置文本可组合项内容
                        text("滑动到顶部")
                    }
                }
                // Button.onClick() 用于处理点击事件
                onClick {
                    // LazyListState.animateScrollToItem() 用于将列表滚动到指定索引项
                    lazyListState.animateScrollToItem(0, 0)
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