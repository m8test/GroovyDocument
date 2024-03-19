## 概况

[CompositionLocal](/API/UI/Compose/CompositionLocal/CompositionLocal/README.md)
用于实现参数的隐式传递,本身不包含任何数据,只会作为键配合 [CompositionLocalProvider](/API/UI/Compose/Widget/CompositionLocalProvider/README.md)
使用. 可通过
[CompositionLocals.compositionLocalOf()](/API/UI/Compose/CompositionLocal/CompositionLocals/README.md?id=compositionLocalOf)
或者 [CompositionLocals.staticCompositionLocalOf()](/API/UI/Compose/CompositionLocal/CompositionLocals/README.md?id=staticCompositionLocalOf)
创建 [ProvidableCompositionLocal](/API/UI/Compose/CompositionLocal/ProvidableCompositionLocal/README.md) ([CompositionLocal](/API/UI/Compose/CompositionLocal/CompositionLocal/README.md)
子类)
,并通过 [ProvidableCompositionLocal.provides()](/API/UI/Compose/CompositionLocal/ProvidableCompositionLocal/README.md?id=provides)
或者 [ProvidableCompositionLocal.providesDefault()](/API/UI/Compose/CompositionLocal/ProvidableCompositionLocal/README.md?id=providesDefault)
提供值与键( [ProvidableCompositionLocal](/API/UI/Compose/CompositionLocal/ProvidableCompositionLocal/README.md))
进行绑定, 在 [Composable](/API/UI/Compose/Widget/Composable/README.md)
中可以通过 [Composable.compositionLocal()](/API/UI/Compose/Widget/Composable/README.md?id=compositionLocal)
获取离当前 [Composable](/API/UI/Compose/Widget/Composable/README.md)
最近 [CompositionLocalProvider](/API/UI/Compose/Widget/CompositionLocalProvider/README.md)
提供的值,如果没有 [CompositionLocalProvider](/API/UI/Compose/Widget/CompositionLocalProvider/README.md)
提供值直接获取,那么会获取到默认值(
创建 [ProvidableCompositionLocal](/API/UI/Compose/CompositionLocal/ProvidableCompositionLocal/README.md)
对象时会提供默认值)