功能:

+ 滚动懒列表,调用此函数以控制滚动并通过
  [ScrollScope.scrollBy()](/API/UI/Compose/State/ScrollableState/ScrollScope/README.md?id=scrollBy)
  获得发送滚动事件的能力。所有更改逻辑滚动位置的操作都必须在滚动块中执行（即使它们没有调用此对象上的任何其他方法），以确保强制执行互斥。如果从其他地方调用 [ScrollableState.scroll()](/API/UI/Compose/State/ScrollableState/README.md?id=scroll)
  , 则将取消此操作。

定义:

+ [Job](/API/Coroutines/Job/README.md) scroll(String scrollPriority, Closure closure)

参数:

+ String scrollPriority - 对状态执行突变的优先级。遵循枚举类值的自然顺序；与另一个值比较为>的值具有更高的优先级。同等或更高优先级的突变将中断当前正在进行的突变。可选值有
    + Default - 突变的默认优先级。可以被其他 Default、UserInput 或 PreventUserInput
      优先级操作中断。默认优先级应用于不应中断用户输入的编程动画或更改。
    + UserInput - 提高了用于实现直接用户交互的突变的优先级。可以被其他 UserInput 或 PreventUserInput 优先级操作中断。
    + PreventUserInput - 只能由其他 PreventUserInput 优先级操作中断的高优先级突变。PreventUserInput 优先级应用于用户输入不应中断的操作。
+ Closure closure - 可执行滚动操作的闭包
    + 参数 - 无
    + delegate - [ScrollScope](/API/UI/Compose/State/ScrollableState/ScrollScope/README.md)

返回值:

+ [Job](/API/Coroutines/Job/README.md) - 协程对象

示例代码:

+ 启动一个Activity, 并通过 [ScrollableState.scroll()](/API/UI/Compose/State/ScrollableState/README.md?id=scroll)
  方法滚动懒列表

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
            // Slot.Button() 用于创建 Button 可组合项
            Button {
                // delegate -> Button
                // Button.content() 用于设置按钮内容
                content {
                    // delegate -> Slot
                    // Slot.Text() 用于创建文本可组合项
                    Text {
                        // delegate -> Text
                        text("滑动")
                    }
                }
                // Button.onClick() 用于处理点击事件
                onClick {
                    // LazyListState.scroll() 用于滚动懒列表
                    lazyListState.scroll("PreventUserInput") {
                        // delegate - ScrollScope
                        // ScrollScope.scrollBy() 用于尝试按像素px向前滚动。
                        scrollBy(100)
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