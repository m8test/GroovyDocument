## 概况

插槽([Slot](/API/UI/Compose/Slot/Slot/README.md))用于添加可组合项([Composable](/API/UI/Compose/Widget/Composable/README.md))
,插槽不会像可组合项那样重组,也就是只会执行一次,所有只要执行一次的操作(例如创建状态,创建协程作用域,创建导航控制器等)都需要在插槽中执行,而不能在可组合项中执行(因为可组合项会重组).

--- 

* [ExposedDropdownMenuBoxScopeSlot](/API/UI/Compose/Slot/ExposedDropdownMenuBoxScopeSlot/README.md)
* [RowScopeSlot](/API/UI/Compose/Slot/RowScopeSlot/README.md)
* [Slot](/API/UI/Compose/Slot/Slot/README.md)