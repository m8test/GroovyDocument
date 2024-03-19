功能:

+ 设置垂直方向排列方式.

定义:

+ [Column](/API/UI/Compose/Widget/Column/README.md) verticalArrangement(String arrangement)

参数:

+ String arrangement - 垂直排列方式,可选值有
    + Top - 垂直放置子对象,使其尽可能靠近主轴的顶部, 视觉: (顶部) 123#### (底部)
    + Bottom - 垂直放置子对象,使其尽可能靠近主轴的底部, 视觉: (顶部) ####123 (底部)
    + Center - 放置子对象时,使其尽可能靠近主轴的中心,视觉: LTR为##123##, RTL为##321##
    + SpaceBetween - 放置子对象时,使它们在主轴上均匀分布,在第一个子对象之前或最后一个子对象之后没有自由空间.视觉: LTR为1##2##3,RTL为3##2##1
    + SpaceAround - 放置子对象时,使它们在主轴上均匀分布,包括第一个子对象之前和最后一个子对象之后的自由空间,但两个连续子对象之间存在的空间量的一半.视觉:
      LTR为#1##2##3#, RTL为#3##2##1#
    + SpaceEvenly - 放置子对象,使其在主轴上均匀分布,包括第一个子对象之前和最后一个子对象之后的自由空间.视觉: LTR为#1#2#3#,RTL为#3#2#1#

返回值:

+ [Column](/API/UI/Compose/Widget/Column/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [Column.verticalArrangement()](/API/UI/Compose/Widget/Column/README.md?id=verticalArrangement)
  方法设置垂直方向排列方式.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.Column() 用于创建 Column 可组合项
    Column {
        // delegate -> Column
        // Column.modifier() 用于修饰 Composable
        modifier {
            // delegate -> Modifier
            // Modifier.fillMaxSize() 用于设置填充父可组合项宽度和高度, 参数为填充父可组合项的比例, 取值区间为 0.0f-1.0f
            fillMaxSize(1.0f)
        }
        // Column.verticalArrangement() 用于设置垂直方向排列方式
        verticalArrangement("Center")
        // Column.content() 用于设置 Column 内容
        content {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("Column")
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