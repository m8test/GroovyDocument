功能:

+ 获取 [MutableStateList](/API/UI/Compose/State/MutableStateList/README.md) 中项目数量

定义:

+ int size()

参数:

+ 无

返回值:

+ int - [MutableStateList](/API/UI/Compose/State/MutableStateList/README.md) 中项目数量

示例代码:

+ 启动一个Activity, 并通过 [MutableStateList.size()](/API/UI/Compose/State/MutableStateList/README.md?id=size)
  方法获取 [MutableStateList](/API/UI/Compose/State/MutableStateList/README.md) 中项目数量

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.mutableStateListOf() 用于创建 MutableStateList
    def listState = mutableStateListOf(null)
    // Slot.Row() 用于创建 Row 可组合项
    Row {
        // delegate -> Row
        // Row.content() 用于设置行内容
        content {
            // delegate -> Slot
            // Slot.LazyColumn() 用于创建 LazyColumn 可组合项
            LazyColumn {
                // delegate -> LazyColumn
                // LazyColumn.withSingleStates() 用于设置可组合项使用到的所有 SingleState
                withSingleStates(listState)
                // LazyList.content() 用于设置列表内容
                content {
                    // delegate -> LazyListScope
                    // LazyListScope.items() 用于添加多个项目到列表中
                    items(listState, { index, value ->
                        "header:$index"
                    }, { index, value ->
                        "headerContent"
                    }) { index, value ->
                        // delegate -> Slot
                        // Slot.Text() 用于创建文本可组合项
                        Text {
                            // delegate -> Text
                            // Text.text() 用于设置文本可组合项内容
                            text("item${value}")
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
                        text("添加项")
                    }
                }
                // Button.onClick() 用于处理点击事件
                onClick {
                    // MutableStateList.size() 用于获取 MutableStateList 中项目数量
                    def listSize = listState.size()
                    // MutableStateList.add() 用于添加项目到 MutableStateList
                    listState.add(listSize)
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
                        text("删除项")
                    }
                }
                // Button.onClick() 用于处理点击事件
                onClick {
                    // MutableStateList.size() 用于获取 MutableStateList 中项目数量
                    def listSize = listState.size() - 1
                    // MutableStateList.remove() 用于删除 MutableStateList 中指定的项目
                    listState.remove(listSize)
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