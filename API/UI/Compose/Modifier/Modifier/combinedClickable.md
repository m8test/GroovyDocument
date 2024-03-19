功能:

+ 配置组件以通过输入或辅助功能“点击”事件接收点击、双击和长按。将此修饰符添加到元素以使其在其范围内可单击。如果您只需要点击处理，不需要双击或长按，请考虑使用 clickable

定义:

+ [Modifier](/API/UI/Compose/Modifier/Modifier/README.md) combinedClickable(boolean enabled, String
  onClickLabel, String role, String
  onLongClickLabel, Closure onLongClick, Closure onDoubleClick, Closure onClick)

参数:

+ boolean enabled - 控制启用状态。当为 false 时, onClick 在元素被点击时不会被执行
+ String onClickLabel - onClick 操作的语义/可访问性标签,可为null
+ String role - 用户界面元素的类型。辅助功能服务可能会使用它来描述元素或进行自定义,可为null
+ String onLongClickLabel - onLongClick 操作的语义/可访问性标签
+ Closure onLongClick - 当用户长按元素时将被调用
    + 参数 - 无
    + delegate - 无
+ Closure onDoubleClick - 将在用户双击元素时调用
    + 参数 - 无
    + delegate - 无
+ Closure onClick - 配置将在用户单击元素时调用的闭包
    + 参数 - 无
    + delegate - 无

返回值:

+ [Modifier](/API/UI/Compose/Modifier/Modifier/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [Modifier.combinedClickable()](/API/UI/Compose/Modifier/Modifier/README.md?id=combinedClickable)
  方法配置组件以通过输入或辅助功能“点击”事件接收点击、双击和长按

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.Column() 用于创建纵向布局
    Column {
        // delegate -> Column
        // Column.content() 用于设置布局内容
        content {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Composable.modifier() 用于配置可组合项的 Modifier ,因为 Text 可组合项继承自 Composable ,所以可以调用 modifier 方法
                modifier {
                    // delegate -> Modifier
                    // Modifier.combinedClickable() 用于配置组件以通过输入或辅助功能“点击”事件接收点击、双击和长按
                    combinedClickable(true, null, null, null, {
                        $console.log("Text被长按")
                    }, {
                        $console.log("Text被双击")
                    }, {
                        $console.log("Text被点击")
                    })
                }
                // Text.text() 用于设置文本可组合项内容
                text("Text")
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