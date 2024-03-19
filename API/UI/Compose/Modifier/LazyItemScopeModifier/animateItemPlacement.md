功能:

+ 为惰性列表中的项目放置设置动画。当您通过
  [LazyListScope.item()](/API/UI/Compose/Widget/LazyList/LazyListScope/README.md?id=item)
  /[LazyListScope.items()](/API/UI/Compose/Widget/LazyList/LazyListScope/README.md?id=items)
  提供键时，此修饰符将启用项目重新排序动画。
  除了项目重新排序之外，由排列或对齐更改等事件引起的所有其他位置更改也将被动画化。

定义:

+ [LazyItemScopeModifier](/API/UI/Compose/Modifier/LazyItemScopeModifier/README.md) animateItemPlacement(
  [FiniteAnimationSpec](/API/UI/Compose/Animation/FiniteAnimationSpec/README.md) animationSpec)

参数:

+ [FiniteAnimationSpec](/API/UI/Compose/Animation/FiniteAnimationSpec/README.md) animationSpec -
  将用于为项目放置设置动画的有限动画。

返回值:

+ [LazyItemScopeModifier](/API/UI/Compose/Modifier/LazyItemScopeModifier/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [LazyItemScopeModifier.animateItemPlacement()](/API/UI/Compose/Modifier/LazyItemScopeModifier/README.md?id=animateItemPlacement)
  方法为惰性列表中的项目放置设置动画

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
                                // Animations.snap() 用于创建一个用于立即将动画值切换为结束值的 AnimationSpec。
                                def animationSpec = $animations.snap(0)
                                // LazyItemScopeModifier.animateItemPlacement() 用于为惰性列表中的项目放置设置动画
                                animateItemPlacement(animationSpec)
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