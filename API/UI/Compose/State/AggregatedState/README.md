## 概况

[AggregatedState](/API/UI/Compose/State/AggregatedState/README.md)
用于表示聚合状态,聚合状态集合了多个状态的值,当这些值发生改变时可以导致 [Composable](/API/UI/Compose/Widget/Composable/README.md)
重组,但需要通过 [Composable.withAggregatedStates()](/API/UI/Compose/Widget/Composable/README.md?id=withAggregatedStates)
将其与 [Composable](/API/UI/Compose/Widget/Composable/README.md) 绑定,其子类有(
后面列举了该状态中值改变会导致 [Composable](/API/UI/Compose/Widget/Composable/README.md) 重组的所有方法)

+ [SnackBarHostState](/API/UI/Compose/State/SnackBarHostState/README.md) -
  [SnackBarHostState.currentSnackBarData()](/API/UI/Compose/State/SnackBarHostState/README.md?id=currentSnackBarData)
+ [LazyListState](/API/UI/Compose/State/LazyListState/README.md) -
  [LazyListState.firstVisibleItemIndex()](/API/UI/Compose/State/LazyListState/README.md?id=firstVisibleItemIndex)
  , [LazyListState.firstVisibleItemScrollOffset()](/API/UI/Compose/State/LazyListState/README.md?id=firstVisibleItemScrollOffset)
  , [LazyListState.isScrollInProgress()](/API/UI/Compose/State/LazyListState/README.md?id=isScrollInProgress)
+ [DismissState](/API/UI/Compose/State/DismissState/README.md) -
  [DismissState.dismissDirection()](/API/UI/Compose/State/DismissState/README.md?id=dismissDirection),
  [DismissState.isDismissed()](/API/UI/Compose/State/DismissState/README.md?id=isDismissed)
+ [DrawerState](/API/UI/Compose/State/DrawerState/README.md) -
  [DrawerState.targetValue()](/API/UI/Compose/State/DrawerState/README.md?id=targetValue)
  , [DrawerState.currentValue()](/API/UI/Compose/State/DrawerState/README.md?id=currentValue),
  [DrawerState.isAnimationRunning()](/API/UI/Compose/State/DrawerState/README.md?id=isAnimationRunning),
  [DrawerState.offset()](/API/UI/Compose/State/DrawerState/README.md?id=offset)
  , [DrawerState.isOpen()](/API/UI/Compose/State/DrawerState/README.md?id=isOpen)
  , [DrawerState.isClosed()](/API/UI/Compose/State/DrawerState/README.md?id=isClosed)
+ [BottomSheetState](/API/UI/Compose/State/BottomSheetState/README.md) -
  [BottomSheetState.isExpanded()](/API/UI/Compose/State/BottomSheetState/README.md?id=isExpanded),
  [BottomSheetState.isCollapsed()](/API/UI/Compose/State/BottomSheetState/README.md?id=isCollapsed)
+ [BackdropScaffoldState](/API/UI/Compose/State/BackdropScaffoldState/README.md) -
  [BackdropScaffoldState.isRevealed()](/API/UI/Compose/State/BackdropScaffoldState/README.md?id=isRevealed)
  , [BackdropScaffoldState.isConcealed()](/API/UI/Compose/State/BackdropScaffoldState/README.md?id=isConcealed)
+ [BottomDrawerState](/API/UI/Compose/State/BottomDrawerState/README.md) -
  [BottomDrawerState.isClosed()](/API/UI/Compose/State/BottomDrawerState/README.md?id=isClosed)
  , [BottomDrawerState.isOpen()](/API/UI/Compose/State/BottomDrawerState/README.md?id=isOpen)
  , [BottomDrawerState.isExpanded()](/API/UI/Compose/State/BottomDrawerState/README.md?id=isExpanded)
+ [ModalBottomSheetState](/API/UI/Compose/State/ModalBottomSheetState/README.md) -
  [ModalBottomSheetState.isVisible()](/API/UI/Compose/State/ModalBottomSheetState/README.md?id=isVisible)
+ [SwipeState](/API/UI/Compose/State/SwipeState/README.md) -
  [SwipeState.isAnimationRunning()](/API/UI/Compose/State/SwipeState/README.md?id=isAnimationRunning),
  [SwipeState.currentValue()](/API/UI/Compose/State/SwipeState/README.md?id=currentValue)
  , [SwipeState.direction()](/API/UI/Compose/State/SwipeState/README.md?id=direction),
  [SwipeState.offset()](/API/UI/Compose/State/SwipeState/README.md?id=offset)
  ,[SwipeState.overflow()](/API/UI/Compose/State/SwipeState/README.md?id=overflow)
  , [SwipeState.targetValue()](/API/UI/Compose/State/SwipeState/README.md?id=targetValue),
  [SwipeState.progress()](/API/UI/Compose/State/SwipeState/README.md?id=progress)