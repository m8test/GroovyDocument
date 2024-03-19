功能:

+ 设置 [LazyListState](/API/UI/Compose/State/LazyListState/README.md) .

定义:

+ [LazyList](/API/UI/Compose/Widget/LazyList/README.md)
  state([LazyListState](/API/UI/Compose/State/LazyListState/README.md) lazyListState)

参数:

+ [LazyListState](/API/UI/Compose/State/LazyListState/README.md) lazyListState - 需要设置的状态对象

返回值:

+ [LazyList](/API/UI/Compose/Widget/LazyList/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [LazyList.state()](/API/UI/Compose/Widget/LazyList/README.md?id=state) 方法设置
  LazyListState .

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