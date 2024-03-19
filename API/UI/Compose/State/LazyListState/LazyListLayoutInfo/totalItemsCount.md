功能:

+ 获取传递到 [LazyColumn](/API/UI/Compose/Widget/LazyColumn/README.md)
  或 [LazyRow](/API/UI/Compose/Widget/LazyRow/README.md) 的项目总数

定义:

+ int totalItemsCount()

参数:

+ 无

返回值:

+ int - 项目总数

示例代码:

+ 启动一个Activity,
  并通过 [LazyListLayoutInfo.totalItemsCount()](/API/UI/Compose/State/LazyListState/LazyListLayoutInfo/README.md?id=totalItemsCount)
  方法获取传递到 [LazyColumn](/API/UI/Compose/Widget/LazyColumn/README.md)
  或 [LazyRow](/API/UI/Compose/Widget/LazyRow/README.md) 的项目总数

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.newLazyListState() 用于创建 LazyListState
    def lazyListState = newLazyListState {
        // delegate -> LazyListState
    }
    // Slot.mutableStateOf() 用于创建一个 MutableState 对象
    def mutableState = mutableStateOf(0)
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
                        // Text.withSingleStates() 用于设置可组合项使用到的所有 SingleState
                        withSingleStates(mutableState)
                        text("totalItemsCount:" + mutableState.value())
                    }
                }
                // Button.onClick() 用于处理点击事件
                onClick {
                    // LazyListState.layoutInfo() 用于获取 LazyListLayoutInfo 对象
                    def layoutInfo = lazyListState.layoutInfo()
                    // LazyListLayoutInfo.totalItemsCount() 用于获取传递到 LazyColumn 或 LazyRow 的项目总数。
                    def count = layoutInfo.totalItemsCount()
                    // MutableState.value() 用于设置 MutableState 对象的值.
                    mutableState.value(count)
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