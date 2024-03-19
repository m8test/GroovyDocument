功能:

+ 设置 [RangeSlider](/API/UI/Compose/Widget/RangeSlider/README.md) 是否启用

定义:

+ [RangeSlider](/API/UI/Compose/Widget/RangeSlider/README.md) enabled(boolean enabled)

参数:

+ boolean enabled - true表示启用,false表示不启用

返回值:

+ [RangeSlider](/API/UI/Compose/Widget/RangeSlider/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [RangeSlider.enabled()](/API/UI/Compose/Widget/RangeSlider/README.md?id=enabled)
  方法设置 [RangeSlider](/API/UI/Compose/Widget/RangeSlider/README.md) 是否启用

```groovy
def MyRangeSlider = { startState, endState, isEnabled ->
    // delegate -> Slot
    // Slot.RangeSlider() 用于创建 RangeSlider 可组合项
    RangeSlider {
        // delegate -> RangeSlider
        // RangeSlider.withSingleStates() 用于设置可组合项使用到的所有 SingleState
        withSingleStates(startState, endState)
        // RangeSlider.enabled() 用于设置 RangeSlider 是否启用
        enabled(isEnabled)
        // RangeSlider.value() 用于设置 RangeSlider 值
        value {
            // delegate -> ClosedRange
            // ClosedRange.start() 用于设置起始值
            start(startState.value())
            // ClosedRange.end() 用于设置结束值
            end(endState.value())
        }
        // RangeSlider.onValueChange() 用于设置 RangeSlider 值改变时的监听事件
        onValueChange {
            // delegate -> ClosedRange
            // ClosedRange.start() 用于获取起始值
            startState.value(it.start())
            // ClosedRange.end() 用于获取结束值
            endState.value(it.end())
        }
        // RangeSlider.valueRange() 用于设置 RangeSlider 取值范围
        valueRange {
            // delegate -> ClosedRange
            // ClosedRange.start() 用于设置起始值
            start(0.0f)
            // ClosedRange.end() 用于设置结束值
            end(100.0f)
        }
        // RangeSlider.steps() 用于设置 RangeSlider 增量
        steps(0)
        // RangeSlider.onValueChangeFinished() 用于设置 RangeSlider 值改变结束时监听事件
        onValueChangeFinished {
            $console.log("值改变结束")
        }
    }
}

// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.mutableStateOf() 用于创建一个 MutableState 对象
    def startState = mutableStateOf(0.0f)
    def endState = mutableStateOf(0.0f)
    // Slot.Column() 用于创建 Column 可组合项
    Column {
        // delegate -> Column
        // Column.content() 用于设置 Column 可组合项中的内容
        content {
            // delegate -> Slot
            MyRangeSlider.delegate = delegate
            MyRangeSlider(startState, endState, true)
            MyRangeSlider(startState, endState, false)
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