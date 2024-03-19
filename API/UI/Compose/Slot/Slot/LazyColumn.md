功能:

+ 创建 [LazyColumn](/API/UI/Compose/Widget/LazyColumn/README.md) 可组合项

定义:

+ [Slot](/API/UI/Compose/Slot/Slot/README.md) LazyColumn(Closure closure)

参数:

+ Closure closure - 设置 [LazyColumn](/API/UI/Compose/Widget/LazyColumn/README.md) 的闭包
    + 参数 - 无
    + delegate - [LazyColumn](/API/UI/Compose/Widget/LazyColumn/README.md)

返回值:

+ [Slot](/API/UI/Compose/Slot/Slot/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [Slot.LazyColumn()](/API/UI/Compose/Slot/Slot/README.md?id=LazyColumn)
  方法创建 [LazyColumn](/API/UI/Compose/Widget/LazyColumn/README.md) 可组合项

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.LazyColumn() 用于创建 LazyColumn 可组合项
    LazyColumn {
        // delegate -> LazyColumn
        // LazyColumn.modifier() 用于修饰 Composable
        modifier {
            // delegate -> Modifier
            // Modifier.fillMaxSize() 用于设置填充父可组合项宽度和高度, 参数为填充父可组合项的比例, 取值区间为 0.0f-1.0f
            fillMaxSize(1.0f)
        }
        // LazyColumn.horizontalAlignment() 用于设置列表水平方向对齐方式
        horizontalAlignment("CenterHorizontally")
        // LazyList.content() 用于设置列表内容
        content {
            // delegate -> LazyListScope
            // LazyListScope.item() 用于添加单个项目到列表中
            item {
                // delegate -> Slot
                // Slot.Text() 用于创建文本可组合项
                Text {
                    // delegate -> Text
                    // Text.text() 用于设置文本可组合项内容
                    text("item")
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