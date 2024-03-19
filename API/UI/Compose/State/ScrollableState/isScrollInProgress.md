功能:

+ 获取此 [ScrollableState](/API/UI/Compose/State/ScrollableState/README.md) 当前是否通过手势,投掷或编程方式滚动。

定义:

+ boolean isScrollInProgress()

参数:

+ 无

返回值:

+ boolean - true表示当前 [ScrollableState](/API/UI/Compose/State/ScrollableState/README.md) 正在滚动,false表示当前 [ScrollableState](/API/UI/Compose/State/ScrollableState/README.md) 不滚动.

示例代码:

+ 启动一个Activity,
  并通过 [ScrollableState.isScrollInProgress()](/API/UI/Compose/State/ScrollableState/README.md?id=isScrollInProgress)
  方法获取此 [ScrollableState](/API/UI/Compose/State/ScrollableState/README.md) 当前是否通过手势,投掷或编程方式滚动

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
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.withAggregatedStates() 用于设置可组合项重组需要的聚合状态
                withAggregatedStates((lazyListState): ["isScrollInProgress"])
                // LazyListState.isScrollInProgress() 用于获取此 ScrollableState 当前是否通过手势,投掷或编程方式滚动
                def index = lazyListState.isScrollInProgress()
                text("isScrollInProgress:$index")
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