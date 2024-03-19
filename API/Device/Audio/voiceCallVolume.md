功能1:

+ 设置通话音量.

定义1:

+ [Audio](/API/Device/Audio/README.md) voiceCallVolume(int volume)

参数1:

+ int volume - 需要设置的音量值

返回值1:

+ [Audio](/API/Device/Audio/README.md) - 返回对象本身方便链式调用

功能2:

+ 获取当前通话音量.

定义2:

+ int voiceCallVolume()

参数2:

+ 无

返回值2:

+ int - 当前通话音量

示例代码:

+ 通过 [Audio.voiceCallVolume()](/API/Device/Audio/README.md?id=voiceCallVolume) 设置/获取通话音量

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.audio() 用于获取Audio对象
def audio = $device.audio()
// Audio.voiceCallVolume(int) 用于设置通话音量
audio.voiceCallVolume(1)
// Audio.voiceCallVolume() 用于获取通话音量
$assert.assertTrue(audio.voiceCallVolume() == 1, "通话音量为1")
// Audio.voiceCallMaxVolume() 用于获取通话最大音量
def voiceCallMaxVolume = audio.voiceCallMaxVolume()
// Audio.voiceCallVolume(int) 用于设置通话音量
audio.voiceCallVolume(voiceCallMaxVolume)
// Audio.voiceCallVolume() 用于获取通话音量
$assert.assertTrue(audio.voiceCallVolume() == voiceCallMaxVolume, "最大通话音量")
```