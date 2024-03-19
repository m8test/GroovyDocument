功能:

+ 添加单个项目到列表中

定义:

+ [LazyListScope](/API/UI/Compose/Widget/LazyList/LazyListScope/README.md) item(Object key = null, Object
  contentType = null, Closure content)

参数:

+ Object key - 设置项目的稳定且唯一的密钥。不允许对列表中的多个项目使用相同的键。密钥的类型应该可以通过 Android 上的 Bundle 保存。如果传递
  null,则列表中的位置将代表键。当您指定键时，滚动位置将根据键保持不变，这意味着如果您在当前可见项目之前添加/删除项目，则具有给定键的项目将保留为第一个可见项目。
+ Object contentType - 此项内容的类型。可以更有效地重复使用相同类型的项目组合。请注意，null 是一种有效类型，此类类型的项目将被视为兼容。
+ Closure content - 项目内容
    + 参数 - 无
    + delegate -
      [Slot](/API/UI/Compose/Slot/Slot/README.md)([LazyItemScopeModifier](/API/UI/Compose/Modifier/LazyItemScopeModifier/README.md))

返回值:

+ [LazyListScope](/API/UI/Compose/Widget/LazyList/LazyListScope/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [LazyListScope.item()](/API/UI/Compose/Widget/LazyList/LazyListScope/README.md?id=item)
  方法添加单个项目到列表中

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.LazyColumn() 用于创建 LazyColumn 可组合项
    LazyColumn {
        // delegate -> LazyColumn
        // LazyList.content() 用于设置列表内容
        content {
            // delegate -> LazyListScope
            // LazyListScope.item() 用于添加单个项目到列表中
            item("key", "contentType") {
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