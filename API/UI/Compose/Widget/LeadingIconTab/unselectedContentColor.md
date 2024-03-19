功能:

+ 设置 [LeadingIconTab](/API/UI/Compose/Widget/LeadingIconTab/README.md) 未被选择时的内容颜色

定义:

+ [LeadingIconTab](/API/UI/Compose/Widget/LeadingIconTab/README.md) unselectedContentColor(Closure closure)

参数:

+ Closure closure - 设置颜色的闭包
    + 参数 - 无
    + delegate - [Color](/API/UI/Compose/Theme/Color/Color/README.md)

返回值:

+ [LeadingIconTab](/API/UI/Compose/Widget/LeadingIconTab/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [LeadingIconTab.unselectedContentColor()](/API/UI/Compose/Widget/LeadingIconTab/README.md?id=unselectedContentColor)
  方法设置 [LeadingIconTab](/API/UI/Compose/Widget/LeadingIconTab/README.md) 未被选择时的内容颜色

```groovy
def MyLeadingIconTab = { state, tabIndex, iconName, tabText ->
    // delegate -> Slot
    // Slot.LeadingIconTab() 用于创建 LeadingIconTab 可组合项
    LeadingIconTab {
        // delegate -> LeadingIconTab
        // LeadingIconTab.withSingleStates() 用于设置可组合项使用到的所有 SingleState
        withSingleStates(state)
        // LeadingIconTab.selected() 用于设置 LeadingIconTab 是否选中
        selected(state.value() == tabIndex)
        // LeadingIconTab.onClick() 用于设置 LeadingIconTab 点击事件
        onClick {
            // 更新状态
            state.value(tabIndex)
        }
        // LeadingIconTab.selectedContentColor() 用于设置 LeadingIconTab 被选择时的内容颜色
        selectedContentColor {
            // delegate -> Color
            // Color.red() 用于配置红色通道
            red(255)
        }
        // LeadingIconTab.unselectedContentColor() 用于设置 LeadingIconTab 未被选择时的内容颜色
        unselectedContentColor {
            // delegate -> Color
            // Color.green() 用于配置绿色通道
            green(255)
        }
        // LeadingIconTab.icon() 用于设置 LeadingIconTab 图标
        icon {
            // delegate -> Slot
            // Slot.Icon() 用于创建 Icon 可组合项
            Icon {
                // delegate -> Icon
                // Icon.vector() 用于设置图标矢量图
                vector("Filled", iconName)
            }
        }
        // LeadingIconTab.text() 用于设置 LeadingIconTab 文本
        text {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text(tabText)
            }
        }
    }
}
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.mutableStateOf() 用于创建一个 MutableState 对象
    def state = mutableStateOf(0)
    // Slot.TabRow() 用于创建 TabRow 可组合项
    TabRow {
        // delegate -> TabRow
        // TabRow.withSingleStates() 用于设置可组合项使用到的所有 SingleState
        withSingleStates(state)
        // TabRow.selectedTabIndex() 用于设置当前被选择的选项卡索引
        selectedTabIndex(state.value())
        // TabRow.tabs() 用于设置选项卡内容
        tabs {
            // delegate -> Slot
            MyLeadingIconTab.delegate = delegate
            MyLeadingIconTab(state, 0, "Home", "主页")
            MyLeadingIconTab(state, 1, "Settings", "设置")
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