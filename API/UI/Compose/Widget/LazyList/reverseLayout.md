功能:

+ 设置是否反转滚动和布局方向,如果为true,项目以相反的顺序排列并且
  [LazyListState.firstVisibleItemIndex()](/API/UI/Compose/State/LazyListState/README.md?id=firstVisibleItemIndex)
  == 0 表示滚动到底部

定义:

+ [LazyList](/API/UI/Compose/Widget/LazyList/README.md) reverseLayout(boolean value)

参数:

+ boolean value - true表示反转,false表示不反转

返回值:

+ [LazyList](/API/UI/Compose/Widget/LazyList/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [LazyList.reverseLayout()](/API/UI/Compose/Widget/LazyList/README.md?id=reverseLayout)
  方法设置是否反转滚动和布局方向

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.LazyColumn() 用于创建 LazyColumn 可组合项
    LazyColumn {
        // delegate -> LazyColumn
        // LazyList.reverseLayout() 用于设置是否反转滚动和布局方向
        reverseLayout(true)
        // LazyList.content() 用于设置列表内容
        content {
            // delegate -> LazyListScope
            // LazyListScope.items() 用于添加多个项目到列表中
            items(10) { index, value ->
                // delegate -> Slot
                // Slot.Text() 用于创建文本可组合项
                Text {
                    // delegate -> Text
                    // Text.text() 用于设置文本可组合项内容
                    text("item$index")
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