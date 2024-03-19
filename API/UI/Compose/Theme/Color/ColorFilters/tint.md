功能:

+ 创建 [ColorFilter](/API/UI/Compose/Theme/Color/ColorFilter/README.md)
  对象，应用作为第二个参数给出的混合模式。源颜色是作为第一个参数给出的颜色，目标颜色是来自正在合成的图层的颜色。然后根据 blendMode
  将此滤镜的输出合成到背景中，使用此滤镜的输出作为源，将背景作为目标。

定义:

+ [ColorFilter](/API/UI/Compose/Theme/Color/ColorFilter/README.md) tint(Closure closure, String blendMode)

参数:

+ Closure closure - 用于设置颜色的闭包
    + 参数 - 无
    + delegate - [Color](/API/UI/Compose/Theme/Color/Color/README.md)
+ String blendMode - 将色调颜色合成到目标时使用的混合模式,可选值有
    + Clear - 删除源图像和目标图像，不留下任何东西。
    + Src - 放下目标图像，只绘制源图像。从概念上讲，首先清除目标，然后绘制源图像。
    + Dst - 放下源图像，只绘制目标图像。从概念上讲，源图像被丢弃，而目标保持不变。
    + SrcOver - 在目标图像上合成源图像。这是默认值。 它代表了最直观的情况，其中形状绘制在下方的顶部，透明区域显示目标层。
    + DstOver - 在目标图像下合成源图像。这与 SrcOver 相反。这在源图像应该在目标图像之前绘制但不能这样做时很有用。
    + SrcIn - 显示源图像，但仅在两个图像重叠的地方显示。 不渲染目标图像，它仅被视为蒙版。 目标的颜色通道被忽略，只有不透明度有影响。要改为显示目标图像，请考虑
      DstIn。要反转掩码的语义（仅显示目标不存在的源，而不是目标存在的位置），请考虑 SrcOut。
    + DstIn - 显示目标图像，但仅在两个图像重叠的地方显示。 不渲染源图像，仅将其视为蒙版。 源的颜色通道被忽略，只有不透明度有影响。要改为显示源图像，请考虑
      SrcIn。要反转掩码的语义（仅显示目标存在的源，而不是目标不存在的位置），请考虑 DstOut。
    + SrcOut - 显示源图像，但仅在两个图像不重叠的地方显示。 不渲染目标图像，它仅被视为蒙版。 目标的颜色通道被忽略，只有不透明度有影响。要改为显示目标图像，请考虑
      DstOut。要反转掩码的语义（仅显示目标存在的源，而不是目标不存在的位置），请考虑 SrcIn。这对应于“Source out Destination”Porter-Duff 运算符。
    + DstOut - 显示目标图像，但仅在两个图像不重叠的地方显示。 不渲染源图像，仅将其视为蒙版。 源的颜色通道被忽略，只有不透明度有影响。要改为显示源图像，请考虑
      SrcOut。要反转掩码的语义（仅显示源存在的目的地，而不是源不存在的位置），请考虑 DstIn。这对应于“Destination out Source”Porter-Duff 运算符。
    + SrcAtop - 将源图像合成到目标图像上，但仅在它与目标图像重叠的地方合成。这本质上是 SrcOver
      运算符，但输出的不透明通道设置为目标图像的不透明通道，而不是两个图像的不透明通道的组合。对于目标位于顶部而不是源位于顶部的变体，请参阅 DstAtop。
    + DstAtop - 将目标图像合成在源图像上，但仅在它与源图像重叠的地方合成。这本质上是 DstOver
      运算符，但输出的不透明度通道设置为源图像的不透明度通道，而不是两个图像的不透明度通道的组合。对于源位于顶部而不是目标位于顶部的变体，请参阅 SrcAtop。
    + Xor - 对源图像和目标图像应用按位异或运算符。 这会在它们重叠的地方留下透明度。
    + Plus - 对源图像和目标图像的组件求和。其中一幅图像的像素的透明度降低了该图像对相应输出像素的贡献，就好像该图像中该像素的颜色更暗一样。
    + Modulate - 将源图像和目标图像的颜色分量相乘。这只能产生相同或更暗的颜色（乘以白色 1.0，结果不变；乘以黑色
      0.0，结果为黑色）。合成两个不透明图像时，这与在投影仪上重叠两个透明胶片具有类似的效果。对于也乘以 alpha 通道的变体，请考虑乘法。
    + Screen - 将源图像和目标图像的组件的倒数相乘，并将结果取反。反转组件意味着完全饱和的通道（不透明的白色）被视为值 0.0，而通常被视为 0.0（黑色、透明）的值被视为
      1.0。这在本质上与调制混合模式相同，但颜色值在乘法之前反转，结果在渲染之前反转。这只能产生相同或更浅的颜色（乘以黑色 1.0，结果不变；乘以白色 0.0，结果为白色）。 同样，在
      alpha 通道中，它只能产生更不透明的颜色。这与两台投影仪同时在同一屏幕上显示其图像具有相似的效果。
    + Overlay -
      在调整源图像和目标图像的组件以支持目标后，将它们相乘。具体来说，如果目标值较小，则将其与源值相乘，而如果源值较小，则将源值的倒数与目标值的倒数相乘，然后反转结果。反转组件意味着完全饱和的通道（不透明的白色）被视为值
      0.0，而通常被视为 0.0（黑色、透明）的值被视为 1.0。
    + Darken - 通过从每个颜色通道中选择最低值来合成源图像和目标图像。输出图像的不透明度以与 SrcOver 相同的方式计算。
    + Lighten - 通过从每个颜色通道中选择最高值来合成源图像和目标图像。输出图像的不透明度以与 SrcOver 相同的方式计算。
    + ColorDodge - 将目标除以源的倒数。反转组件意味着完全饱和的通道（不透明的白色）被视为值 0.0，而通常被视为 0.0（黑色、透明）的值被视为 1.0。注意: 此
      BlendMode 只能在 Android API 级别 29 及更高版本上使用
    + ColorBurn - 将目标的倒数除以源，然后倒数结果。反转组件意味着完全饱和的通道（不透明的白色）被视为值 0.0，而通常被视为 0.0（黑色、透明）的值被视为 1.0。注意: 此
      BlendMode 只能在 Android API 级别 29 及更高版本上使用
    + Hardlight -
      在调整源图像和目标图像的组件以支持源图像后，将它们相乘。具体来说，如果源值较小，则将其与目标值相乘，如果目标值较小，则将目标值的倒数与源值的倒数相乘，然后反转结果。反转组件意味着完全饱和的通道（不透明的白色）被视为值
      0.0，而通常被视为 0.0（黑色、透明）的值被视为 1.0。注意: 此 BlendMode 只能在 Android API 级别 29 及更高版本上使用
    + Softlight - 对低于 0.5 的源值使用 ColorDodge，对高于 0.5 的源值使用 ColorBurn。这会产生与叠加类似但更柔和的效果。注意: 此 BlendMode
      只能在 Android API 级别 29 及更高版本上使用
    + Difference - 从每个通道的较大值中减去较小的值。合成黑色没有效果； 合成白色会反转另一幅图像的颜色。输出图像的不透明度以与 SrcOver 相同的方式计算。注意: 此
      BlendMode 只能在 Android API 级别 29 及更高版本上使用. 效果类似于 Exclusion ，但更严厉。
    + Exclusion - 从两幅图像的总和中减去两幅图像乘积的两倍。合成黑色没有效果； 合成白色会反转另一幅图像的颜色。输出图像的不透明度以与 SrcOver 相同的方式计算。注意: 此
      BlendMode 只能在 Android API 级别 29 及更高版本上使用. 效果类似于 Difference，但更柔和。
    + Multiply - 将源图像和目标图像的组件相乘，包括 Alpha 通道。这只能产生相同或更暗的颜色（乘以白色 1.0，结果不变；乘以黑色 0.0，结果为黑色）。由于 alpha
      通道也相乘，因此一幅图像中的完全透明像素（不透明度 0.0）会导致输出中的完全透明像素。 这类似于 DstIn，但颜色组合。对于乘以颜色但不乘以 alpha 通道的变体，请考虑调制。注意:
      此 BlendMode 只能在 Android API 级别 29 及更高版本上使用
    + Hue - 获取源图像的色调，以及目标图像的饱和度和亮度。效果是用源图像对目标图像进行着色。输出图像的不透明度以与 SrcOver 相同的方式计算。
      源图像中完全透明的区域采用目标图像的色调。注意: 此 BlendMode 只能在 Android API 级别 29 及更高版本上使用
    + Saturation - 获取源图像的饱和度，以及目标图像的色调和亮度。输出图像的不透明度以与 SrcOver 相同的方式计算。 源图像中完全透明的区域从目标图像中获取饱和度。注意: 此
      BlendMode 只能在 Android API 级别 29 及更高版本上使用
    + Color - 获取源图像的色调和饱和度，以及目标图像的亮度。效果是用源图像对目标图像进行着色。输出图像的不透明度以与 SrcOver 相同的方式计算。
      源图像中完全透明的区域采用目标图像的色调和饱和度。注意: 此 BlendMode 只能在 Android API 级别 29 及更高版本上使用
    + Luminosity - 获取源图像的亮度，以及目标图像的色调和饱和度。输出图像的不透明度以与 SrcOver 相同的方式计算。 源图像中完全透明的区域从目标中获取它们的亮度。注意: 此
      BlendMode 只能在 Android API 级别 29 及更高版本上使用

返回值:

+ [ColorFilter](/API/UI/Compose/Theme/Color/ColorFilter/README.md) -
  新创建的 [ColorFilter](/API/UI/Compose/Theme/Color/ColorFilter/README.md) 对象

示例代码:

+ 启动一个Activity, 并通过 [ColorFilters.tint()](/API/UI/Compose/Theme/Color/ColorFilters/README.md?id=tint)
  方法创建 [ColorFilter](/API/UI/Compose/Theme/Color/ColorFilter/README.md) 对象

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.AsyncImage() 用于创建 AsyncImage 可组合项
    AsyncImage {
        // delegate -> AsyncImage
        // ColorFilters.tint() 用于创建 ColorFilter 对象
        def cf = $colorFilters.tint({
            // delegate -> Color
            // Color.red() 用于配置红色通道
            red(255)
        }, "SrcIn")
        // AsyncImage.colorFilter() 用于设置 ColorFilter
        colorFilter(cf)
        // AsyncImage.request() 用于设置图片请求
        request {
            // delegate -> ImageRequest
            def resources = $applicationContext.getResources()
            // ImageRequest.drawable() 用于设置从 Drawable 中读取图片
            drawable(resources.getDrawable(resources.getIdentifier("ic_baseline_android_24", "drawable", $applicationContext.getPackageName())))
            // ImageRequest.format() 用于设置图片格式
            format("svg")
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