## 概况

[DisposableEffect](/API/UI/Compose/Effects/DisposableEffect/README.md)
中 [DisposableEffect.effect()](/API/UI/Compose/Effects/DisposableEffect/README.md?id=effect)
内容在进入组合时会执行,但是 [DisposableEffect.effect()](/API/UI/Compose/Effects/DisposableEffect/README.md?id=effect) 内中的
[DisposableEffectScope.onDispose()](/API/UI/Compose/Effects/DisposableEffect/DisposableEffectScope/README.md?id=onDispose)
不会被执行, [DisposableEffectScope.onDispose()](/API/UI/Compose/Effects/DisposableEffect/DisposableEffectScope/README.md?id=onDispose)
会在 [DisposableEffect](/API/UI/Compose/Effects/DisposableEffect/README.md)
离开组合时执行,继承自 [Composable](/API/UI/Compose/Widget/Composable/README.md)

## effect()

[effect](effect.md ":include")
