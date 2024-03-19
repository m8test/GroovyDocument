功能:

+ 设置列表水平方向排列方式.

定义:

+ [LazyRow](/API/UI/Compose/Widget/LazyRow/README.md) horizontalArrangement(String arrangement)

参数:

+ String arrangement - 水平排列方式,可选值有
    + Start - 水平放置子项，使其尽可能靠近水平轴的起点（如果布局方向为 LTR，则为左侧，否则为右侧）。 视觉上：LTR 为 123####，####321。
    + End - 将子项水平放置，使他们尽可能靠近主轴的末端。 视觉上：LTR 为 ####123，RTL 为 321####。
    + Center - 将子项放置在尽可能靠近主轴中心的位置。 视觉上：LTR 为##123##，RTL 为##321##。
    + SpaceBetween - 放置子项，使它们在主轴上均匀分布，在第一个子项之前或最后一个子项之后没有可用空间。 视觉上：LTR 为 1##2##3，RTL 为 3##2##1。
    + SpaceAround - 放置子项时，使它们在主轴上均匀分布，包括第一个子项之前和最后一个子项之后的自由空间，但两个连续子项之间存在的空间量的一半。 视觉上：#1##2##3# 用于
      LTR，#3##2##1# 用于 RTL
    + SpaceEvenly - 放置子项，使它们在主轴上均匀分布，包括第一个子项之前和最后一个子项之后的自由空间。 视觉上：#1#2#3# 用于 LTR，#3#2#1# 用于 RTL。

返回值:

+ [LazyRow](/API/UI/Compose/Widget/LazyRow/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [LazyRow.horizontalArrangement()](/API/UI/Compose/Widget/LazyRow/README.md?id=horizontalArrangement)
  方法设置列表水平方向排列方式.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.LazyRow() 用于创建 LazyRow 可组合项
    LazyRow {
        // delegate -> LazyRow
        // LazyRow.modifier() 用于修饰 Composable
        modifier {
            // delegate -> Modifier
            // Modifier.fillMaxSize() 用于设置填充父可组合项宽度和高度, 参数为填充父可组合项的比例, 取值区间为 0.0f-1.0f
            fillMaxSize(1.0f)
        }
        // LazyRow.horizontalArrangement() 用于设置列表水平方向排列方式
        horizontalArrangement("Center")
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