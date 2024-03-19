## 概况

[SingleState](/API/UI/Compose/State/SingleState/README.md) 表示单一状态,
如果需要让 [Composable](/API/UI/Compose/Widget/Composable/README.md)
随着 [SingleState](/API/UI/Compose/State/SingleState/README.md) 的值改变而重组,
那么需要通过 [Composable.withSingleStates()](/API/UI/Compose/Widget/Composable/README.md?id=withSingleStates)
将其绑定到 [Composable](/API/UI/Compose/Widget/Composable/README.md) 上.
[SingleState](/API/UI/Compose/State/SingleState/README.md) 继承自 [State](/API/UI/Compose/State/State/README.md) ,其子类有

+ [MutableState](/API/UI/Compose/State/MutableState/README.md)
+ [MutableStateList](/API/UI/Compose/State/MutableStateList/README.md)