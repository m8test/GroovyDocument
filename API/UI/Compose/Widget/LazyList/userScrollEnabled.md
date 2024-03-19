功能:

+ 设置是否允许通过用户手势或可访问性操作进行滚动。 即使它被禁用，您仍然可以使用状态以编程方式滚动。

定义:

+ [LazyList](/API/UI/Compose/Widget/LazyList/README.md) userScrollEnabled(boolean value)

参数:

+ boolean value - true表示允许手势滑动,false表示不允许手势滑动

返回值:

+ [LazyList](/API/UI/Compose/Widget/LazyList/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [LazyList.userScrollEnabled()](/API/UI/Compose/Widget/LazyList/README.md?id=userScrollEnabled)
  方法设置是否允许通过用户手势或可访问性操作进行滚动

```groovy
def MyButton = { btnText, onButtonClick ->
    // delegate -> Slot
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
                text(btnText)
            }
        }
        // Button.onClick() 用于处理点击事件
        onClick {
            onButtonClick()
        }
    }
}

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
                    // LazyListScope.userScrollEnabled() 用于设置是否允许通过用户手势或可访问性操作进行滚动
                    userScrollEnabled(false)
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
            // Slot.Column() 用于创建 Column 可组合项
            Column {
                // delegate -> Column
                // Column.content() 用于设置 Column 可组合项中的内容
                content {
                    // delegate -> Slot
                    MyButton.delegate = delegate
                    MyButton("滑动到顶部") {
                        // LazyListState.animateScrollToItem() 用于将列表滚动到指定索引项
                        lazyListState.animateScrollToItem(0, 0)
                    }
                    MyButton("滑动到底部") {
                        // LazyListState.animateScrollToItem() 用于将列表滚动到指定索引项
                        lazyListState.animateScrollToItem(99, 0)
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