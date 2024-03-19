功能:

+ 将列表滚动到指定索引项。

定义:

+ [Job](/API/Coroutines/Job/README.md) animateScrollToItem(int index, int scrollOffset)

参数:

+ int index - 要滚动到的索引。必须为非负。
+ int scrollOffset - 滚动后项目应结束的偏移量。请注意，正偏移是指向前滚动，因此在从上到下的列表中，正偏移将进一步向上滚动项目（使其部分离开屏幕）。

返回值:

+ [Job](/API/Coroutines/Job/README.md) - 协程对象

示例代码:

+ 启动一个Activity,
  并通过 [LazyListState.animateScrollToItem()](/API/UI/Compose/State/LazyListState/README.md?id=animateScrollToItem)
  方法将列表滚动到指定索引项

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
                    // LazyListState.animateScrollToItem() 用于将列表滚动到指定索引项
                    lazyListState.animateScrollToItem(10, 10)
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