## 概况

断言是一种放在程序中的一阶逻辑,目的是为了标示与验证程序开发者预期的结果－当程序运行到断言的位置时,对应的断言应该为真(假).若断言不为真(假)时,程序会中止运行,并给出错误消息.断言有以下类型:

+ [Assert.assertTrue](/API/Assert/Assert/README.md?id=assertTrue) : 断言条件为真
+ [Assert.assertFalse](/API/Assert/Assert/README.md?id=assertFalse) : 断言条件为假

## 断言真

[Assert.assertTrue](/API/Assert/Assert/README.md?id=assertTrue) 用于断言条件为真,如果条件为假则抛出 AssertionError .

[filename](assertTrue.md ':include')

## 断言假

[Assert.assertFalse](/API/Assert/Assert/README.md?id=assertFalse) 用于断言条件为假,如果条件为真则抛出 AssertionError
.

[filename](assertFalse.md ':include')