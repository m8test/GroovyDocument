功能:

+ 设置列表内容边距.

定义:

+ [LazyList](/API/UI/Compose/Widget/LazyList/README.md) contentPadding(Closure closure)

参数:

+ Closure closure - 设置内容边距的闭包
    + 参数 - 无
    + delegate - [PaddingValues](/API/UI/Compose/Graphics/PaddingValues/README.md)

返回值:

+ [LazyList](/API/UI/Compose/Widget/LazyList/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [LazyList.contentPadding()](/API/UI/Compose/Widget/LazyList/README.md?id=contentPadding)
  方法设置列表内容边距.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.LazyColumn() 用于创建 LazyColumn 可组合项
    LazyColumn {
        // delegate -> LazyColumn
        // LazyList.contentPadding() 用于设置列表内容边距
        contentPadding {
            // delegate -> PaddingValues
            // PaddingValues.all() 用于同时设置上下左右四个方向边距
            all(20)
        }
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