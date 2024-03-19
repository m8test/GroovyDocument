## 概况

[StaticProvidableCompositionLocal](/API/UI/Compose/CompositionLocal/StaticProvidableCompositionLocal/README.md)
实例对象可通过 [CompositionLocals.staticCompositionLocalOf()](/API/UI/Compose/CompositionLocal/CompositionLocals/README.md?id=staticCompositionLocalOf)
方法创建,如果其通过 [provides()](/API/UI/Compose/CompositionLocal/ProvidableCompositionLocal/README.md?id=provides)
或者 [providesDefault()](/API/UI/Compose/CompositionLocal/ProvidableCompositionLocal/README.md?id=providesDefault)
方法提供值并且该值为 [SingleState](/API/UI/Compose/State/SingleState/README.md) 时,若该 [SingleState](/API/UI/Compose/State/SingleState/README.md) 通过
[SingleState.value()](/API/UI/Compose/State/SingleState/README.md?id=value)
改变值,那么 [CompositionLocalProvider.content()](/API/UI/Compose/Widget/CompositionLocalProvider/README.md?id=content)
中的所有 [Composable](/API/UI/Compose/Widget/Composable/README.md) 都会重组,
继承自 [ProvidableCompositionLocal](/API/UI/Compose/CompositionLocal/ProvidableCompositionLocal/README.md)