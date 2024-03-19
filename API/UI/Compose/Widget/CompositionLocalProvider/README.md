## 概况

[CompositionLocalProvider](/API/UI/Compose/Widget/CompositionLocalProvider/README.md)
将值绑定到 [ProvidableCompositionLocal](/API/UI/Compose/CompositionLocal/ProvidableCompositionLocal/README.md)
键,作用是在 [Composable](/API/UI/Compose/Widget/Composable/README.md) 中隐式传递参数。
使用 [Composable.compositionLocal()](/API/UI/Compose/Widget/Composable/README.md?id=compositionLocal) 读取
[ProvidableCompositionLocal](/API/UI/Compose/CompositionLocal/ProvidableCompositionLocal/README.md)
将为在 [CompositionLocalProvider.content()](/API/UI/Compose/Widget/CompositionLocalProvider/README.md?id=content)
中直接或间接调用的所有 [Composable](/API/UI/Compose/Widget/Composable/README.md)
返回 [CompositionLocalProvider.values()](/API/UI/Compose/Widget/CompositionLocalProvider/README.md?id=values)
参数中提供的值,继承自 [Composable](/API/UI/Compose/Widget/Composable/README.md)

## content()

[content](content.md ":include")

## values()

[values](values.md ":include")