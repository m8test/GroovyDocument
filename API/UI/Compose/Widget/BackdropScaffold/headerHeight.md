功能:

+ 设置前层处于非活动状态时的最小高度.

定义:

+ [BackdropScaffold](/API/UI/Compose/Widget/BackdropScaffold/README.md) headerHeight(Number height)

参数:

+ Number height - 需要设置的高度,单位dp

返回值:

+ [BackdropScaffold](/API/UI/Compose/Widget/BackdropScaffold/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [BackdropScaffold.headerHeight()](/API/UI/Compose/Widget/BackdropScaffold/README.md?id=headerHeight)
  方法设置前层处于非活动状态时的最小高度.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.BackdropScaffold() 用于创建 BackdropScaffold 可组合项
    BackdropScaffold {
        // delegate -> BackdropScaffold
        // BackdropScaffold.headerHeight() 用于设置前层处于非活动状态时的最小高度
        headerHeight(50)
        // BackdropScaffold.backLayerContent() 用于设置后层内容
        backLayerContent {
            // delegate -> Slot
            // Slot.LazyColumn() 用于创建 LazyColumn 可组合项
            LazyColumn {
                // delegate -> LazyColumn
                // LazyColumn.content() 用于设置纵向列表内容
                content {
                    // delegate -> LazyListScope
                    // LazyListScope.items() 用于设置列表内容
                    items(100) { index, value ->
                        // delegate -> Slot
                        // Slot.Text() 用于创建文本可组合项
                        Text {
                            // delegate -> Text
                            // Text.text() 用于设置文本可组合项内容
                            text("$index")
                        }
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