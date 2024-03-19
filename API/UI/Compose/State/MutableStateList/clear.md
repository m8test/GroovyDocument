功能:

+ 清空 [MutableStateList](/API/UI/Compose/State/MutableStateList/README.md) 所有项目

定义:

+ [MutableStateList](/API/UI/Compose/State/MutableStateList/README.md) clear()

参数:

+ 无

返回值:

+ [MutableStateList](/API/UI/Compose/State/MutableStateList/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [MutableStateList.clear()](/API/UI/Compose/State/MutableStateList/README.md?id=clear)
  方法清空 [MutableStateList](/API/UI/Compose/State/MutableStateList/README.md) 所有项目

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.mutableStateListOf() 用于创建 MutableStateList
    def listState = mutableStateListOf([0, 1, 2, 3])
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
                    // MutableStateList.add() 用于添加项目到 MutableStateList
                    listState.add(listState.size())
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
                        text("清空项")
                    }
                }
                // Button.onClick() 用于处理点击事件
                onClick {
                    // MutableStateList.clear() 用于清空 MutableStateList 所有项目
                    listState.clear()
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