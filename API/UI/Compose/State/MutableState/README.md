## 概况

[MutableState](/API/UI/Compose/State/MutableState/README.md)
表示单个可变的状态,当通过 [MutableState.value()](/API/UI/Compose/State/MutableState/README.md?id=value)
改变值的时候,所有通过 [Composable.withSingleStates()](/API/UI/Compose/Widget/Composable/README.md?id=withSingleStates)
添加该 [MutableState](/API/UI/Compose/State/MutableState/README.md)
的 [Composable](/API/UI/Compose/Widget/Composable/README.md) 都会重组,
继承自 [SingleState](/API/UI/Compose/State/SingleState/README.md)

## value()

[value](value.md ":include")