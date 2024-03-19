功能:

+ 对 [MutableStateList](/API/UI/Compose/State/MutableStateList/README.md) 中的项目排序

定义:

+ [MutableStateList](/API/UI/Compose/State/MutableStateList/README.md) sortWith(Closure closure)

参数:

+ Closure closure - 用于排序的闭包
    + 参数
        + Object obj1 - 用于比较的对象
        + object obj2 - 用于比较的对象
    + delegate - 无
    + 返回值 - boolean

返回值:

+ [MutableStateList](/API/UI/Compose/State/MutableStateList/README.md) - 删除成功返回true,否则返回false

示例代码:

+ 启动一个Activity,
  并通过 [MutableStateList.sortWith()](/API/UI/Compose/State/MutableStateList/README.md?id=sortWith)
  方法对 [MutableStateList](/API/UI/Compose/State/MutableStateList/README.md) 中的项目排序

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.mutableStateListOf() 用于创建 MutableStateList
    def listState = mutableStateListOf(null)
    // Slot.mutableStateOf() 用于创建一个 MutableState 对象
    def orderState = mutableStateOf(false)
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
                        // Text.withSingleStates() 用于设置可组合项使用到的所有 SingleState
                        withSingleStates(orderState)
                        if (orderState.value()) {
                            // Text.text() 用于设置文本可组合项内容
                            text("升序")
                        } else {
                            // Text.text() 用于设置文本可组合项内容
                            text("降序")
                        }
                    }
                }
                // Button.onClick() 用于处理点击事件
                onClick {
                    if (orderState.value()) {
                        // MutableStateList.sortWith() 用于对 MutableStateList 中的项目排序
                        listState.sortWith { i1, i2 ->
                            i1 - i2
                        }
                    } else {
                        // MutableStateList.sortWith() 用于对 MutableStateList 中的项目排序
                        listState.sortWith { i1, i2 ->
                            i2 - i1
                        }
                    }
                    orderState.value(!orderState.value())
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