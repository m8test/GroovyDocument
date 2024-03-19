功能:

+ 创建 [RangeSlider](/API/UI/Compose/Widget/RangeSlider/README.md) 可组合项

定义:

+ [Slot](/API/UI/Compose/Slot/Slot/README.md) RangeSlider(Closure closure)

参数:

+ Closure closure - 设置 [RangeSlider](/API/UI/Compose/Widget/RangeSlider/README.md) 的闭包
    + 参数 - 无
    + delegate - [RangeSlider](/API/UI/Compose/Widget/RangeSlider/README.md)

返回值:

+ [Slot](/API/UI/Compose/Slot/Slot/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [Slot.RangeSlider()](/API/UI/Compose/Slot/Slot/README.md?id=RangeSlider)
  方法创建 [RangeSlider](/API/UI/Compose/Widget/RangeSlider/README.md) 可组合项

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.mutableStateOf() 用于创建一个 MutableState 对象
    def startState = mutableStateOf(0.0f)
    def endState = mutableStateOf(0.0f)
    // Slot.RangeSlider() 用于创建 RangeSlider 可组合项
    RangeSlider {
        // delegate -> RangeSlider
        // RangeSlider.withSingleStates() 用于设置可组合项使用到的所有 SingleState
        withSingleStates(startState, endState)
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
        // RangeSlider.colors() 用于设置 RangeSlider 颜色
        colors {
            // delegate -> SliderColors
            // SliderColors.thumbColor() 用于设置 Slider 拇指颜色
            thumbColor {
                // delegate -> Color
                // Color.red() 用于配置红色通道
                red(255)
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