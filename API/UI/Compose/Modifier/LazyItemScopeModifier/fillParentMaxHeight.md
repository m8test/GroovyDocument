功能:

+ 通过将最小高度设置为等于最大高度乘以分数. 请注意，默认情况下，分数为
  1，因此修饰符将使内容填充整个父级高度。常规 [Modifier.fillMaxHeight()](/API/UI/Compose/Modifier/Modifier/README.md?id=fillMaxHeight)
  不能在滚动水平布局内工作.

定义:

+ [LazyItemScopeModifier](/API/UI/Compose/Modifier/LazyItemScopeModifier/README.md) fillParentMaxHeight(
  float fraction)

参数:

+ float fraction - 分数,取值范围[0.0-1.0]

返回值:

+ [LazyItemScopeModifier](/API/UI/Compose/Modifier/LazyItemScopeModifier/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [LazyItemScopeModifier.fillParentMaxHeight()](/API/UI/Compose/Modifier/LazyItemScopeModifier/README.md?id=fillParentMaxHeight)
  方法通过将最小高度设置为等于最大高度乘以分数

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
                            // Text.modifier() 用于设置修饰符
                            modifier {
                                // delegate -> LazyItemScopeModifier
                                // LazyItemScopeModifier.fillParentMaxHeight() 用于通过将最小高度设置为等于最大高度乘以分数
                                fillParentMaxHeight(0.5f)
                            }
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