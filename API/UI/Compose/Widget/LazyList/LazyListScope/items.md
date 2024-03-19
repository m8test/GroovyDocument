功能:

+ 添加多个项目到列表中

定义1:

+ [LazyListScope](/API/UI/Compose/Widget/LazyList/LazyListScope/README.md) items(int count, Closure key =
  null, Closure contentType = null, Closure content)

参数1:

+ int count - 添加到列表的项目数量
+ Closure key - 设置项目的稳定且唯一的密钥。不允许对列表中的多个项目使用相同的键。密钥的类型应该可以通过 Android 上的 Bundle 保存。如果传递
  null,则列表中的位置将代表键。当您指定键时，滚动位置将根据键保持不变，这意味着如果您在当前可见项目之前添加/删除项目，则具有给定键的项目将保留为第一个可见项目。
    + 参数
        + int index - 索引值
        + int value - 值
    + delegate - 无
    + 返回值 - Object
+ Object contentType - 此项内容的类型。可以更有效地重复使用相同类型的项目组合。请注意，null 是一种有效类型，此类类型的项目将被视为兼容。
    + 参数
        + int index - 索引值
        + int value - 值
    + delegate - 无
    + 返回值 - Object
+ Closure content - 项目内容
    + 参数
        + int index - 索引值
        + int value - 值
    + delegate -
      [Slot](/API/UI/Compose/Slot/Slot/README.md)([LazyItemScopeModifier](/API/UI/Compose/Modifier/LazyItemScopeModifier/README.md))

返回值1:

+ [LazyListScope](/API/UI/Compose/Widget/LazyList/LazyListScope/README.md) - 返回对象本身方便链式调用

定义2:

+ [LazyListScope](/API/UI/Compose/Widget/LazyList/LazyListScope/README.md) items(List<Object> list, Closure
  key = null, Closure contentType = null, Closure content)

参数2:

+ List\<Object\> list - 需要添加到列表的数据
+ Closure key - 设置项目的稳定且唯一的密钥。不允许对列表中的多个项目使用相同的键。密钥的类型应该可以通过 Android 上的 Bundle 保存。如果传递
  null,则列表中的位置将代表键。当您指定键时，滚动位置将根据键保持不变，这意味着如果您在当前可见项目之前添加/删除项目，则具有给定键的项目将保留为第一个可见项目。
    + 参数
        + int index - 索引值
        + Object value - 值
    + delegate - 无
    + 返回值 - Object
+ Object contentType - 此项内容的类型。可以更有效地重复使用相同类型的项目组合。请注意，null 是一种有效类型，此类类型的项目将被视为兼容。
    + 参数
        + int index - 索引值
        + Object value - 值
    + delegate - 无
    + 返回值 - Object
+ Closure content - 项目内容
    + 参数
        + int index - 索引值
        + Object value - 值
    + delegate -
      [Slot](/API/UI/Compose/Slot/Slot/README.md)([LazyItemScopeModifier](/API/UI/Compose/Modifier/LazyItemScopeModifier/README.md))

返回值2:

+ [LazyListScope](/API/UI/Compose/Widget/LazyList/LazyListScope/README.md) - 返回对象本身方便链式调用

定义3:

+ [LazyListScope](/API/UI/Compose/Widget/LazyList/LazyListScope/README.md)
  items([MutableStateList](/API/UI/Compose/State/MutableStateList/README.md) list, Closure
  key = null, Closure contentType = null, Closure content)

参数3:

+ [MutableStateList](/API/UI/Compose/State/MutableStateList/README.md) list - 需要添加到列表的数据
+ Closure key - 设置项目的稳定且唯一的密钥。不允许对列表中的多个项目使用相同的键。密钥的类型应该可以通过 Android 上的 Bundle 保存。如果传递
  null,则列表中的位置将代表键。当您指定键时，滚动位置将根据键保持不变，这意味着如果您在当前可见项目之前添加/删除项目，则具有给定键的项目将保留为第一个可见项目。
    + 参数
        + int index - 索引值
        + Object value - 值
    + delegate - 无
    + 返回值 - Object
+ Object contentType - 此项内容的类型。可以更有效地重复使用相同类型的项目组合。请注意，null 是一种有效类型，此类类型的项目将被视为兼容。
    + 参数
        + int index - 索引值
        + Object value - 值
    + delegate - 无
    + 返回值 - Object
+ Closure content - 项目内容
    + 参数
        + int index - 索引值
        + Object value - 值
    + delegate -
      [Slot](/API/UI/Compose/Slot/Slot/README.md)([LazyItemScopeModifier](/API/UI/Compose/Modifier/LazyItemScopeModifier/README.md))

返回值3:

+ [LazyListScope](/API/UI/Compose/Widget/LazyList/LazyListScope/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [LazyListScope.items()](/API/UI/Compose/Widget/LazyList/LazyListScope/README.md?id=items) 方法添加多个项目到列表中

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
                    // LazyListScope.stickyHeader() 用于添加一个粘性标题项
                    stickyHeader("header1", "header") {
                        // delegate -> Slot
                        // Slot.Text() 用于创建文本可组合项
                        Text {
                            // delegate -> Text
                            // Text.text() 用于设置文本可组合项内容
                            text("Count")
                        }
                    }
                    // LazyListScope.items() 用于添加多个项目到列表中
                    items(100, { index, value ->
                        "header1:$index"
                    }, { index, value ->
                        "headerContent1"
                    }) { index, value ->
                        // delegate -> Slot
                        // Slot.Text() 用于创建文本可组合项
                        Text {
                            // delegate -> Text
                            // Text.text() 用于设置文本可组合项内容
                            text("item$index")
                        }
                    }
                    // LazyListScope.stickyHeader() 用于添加一个粘性标题项
                    stickyHeader("header2", "header") {
                        // delegate -> Slot
                        // Slot.Text() 用于创建文本可组合项
                        Text {
                            // delegate -> Text
                            // Text.text() 用于设置文本可组合项内容
                            text("List")
                        }
                    }
                    // LazyListScope.items() 用于添加多个项目到列表中
                    items(["a", "b", "c", "d", "e", "f", "g", "h", "i"], { index, value ->
                        "header2:$index"
                    }, { index, value ->
                        "headerContent2"
                    }) { index, value ->
                        // delegate -> Slot
                        // Slot.Text() 用于创建文本可组合项
                        Text {
                            // delegate -> Text
                            // Text.text() 用于设置文本可组合项内容
                            text("item${value}")
                        }
                    }
                    // LazyListScope.stickyHeader() 用于添加一个粘性标题项
                    stickyHeader("header3", "header") {
                        // delegate -> Slot
                        // Slot.Text() 用于创建文本可组合项
                        Text {
                            // delegate -> Text
                            // Text.text() 用于设置文本可组合项内容
                            text("MutableStateList")
                        }
                    }
                    // LazyListScope.items() 用于添加多个项目到列表中
                    items(listState, { index, value ->
                        "header3:$index"
                    }, { index, value ->
                        "headerContent3"
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