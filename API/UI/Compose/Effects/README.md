附带效应是指发生在可组合函数作用域之外的应用状态的变化。由于可组合项的生命周期和属性（例如不可预测的重组、以不同顺序执行可组合项的重组或可以舍弃的重组），可组合项在理想情况下应该是无附带效应的。

不过，有时附带效应是必要的，例如，触发一次性事件（例如显示信息提示控件），或在满足特定状态条件时进入另一个屏幕。这些操作应从能感知可组合项生命周期的受控环境中调用。

效应是一种可组合函数，该函数不会发出界面，并且在组合完成后不会产生附带效应

每次重组后都会运行 [SideEffect](/API/UI/Compose/Effects/SideEffect/README.md)
。要启动可能跨越许多重组的正在进行的任务，请参阅 [LaunchedEffect](/API/UI/Compose/Effects/LaunchedEffect/README.md)
。要管理事件订阅或其他对象生命周期，请参阅 [DisposableEffect](/API/UI/Compose/Effects/DisposableEffect/README.md)。

---

* [DisposableEffect](/API/UI/Compose/Effects/DisposableEffect/README.md)
    * [DisposableEffectScope](/API/UI/Compose/Effects/DisposableEffect/DisposableEffectScope/README.md)
* [LaunchedEffect](/API/UI/Compose/Effects/LaunchedEffect/README.md)
* [SideEffect](/API/UI/Compose/Effects/SideEffect/README.md)