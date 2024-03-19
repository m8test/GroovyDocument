功能:

+ 删除数据库.

定义:

+ boolean dropDatabase(String|Database param)

参数:

+ String|[Database](/API/Database/Database/README.md) param - 可以是数据库路径(String)
  ,也可以是数据库对象([Database](/API/Database/Database/README.md))

返回值:

+ boolean - 如果数据库存在并且删除成功返回true,否则返回false

示例代码:

+ 通过 [Databases.dropDatabase()](/API/Database/Databases/README.md?id=dropDatabase) 删除数据库.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Databases.openOrCreateDatabase() 用于打开/创建数据库
def database = $databases.openOrCreateDatabase("M8Test_test.db")
// Database.createTable() 用于新建一个简单数据表,该表所有列均为text类型,并且存在自增id属性
database.createTable("user", ["username", "password"])
// Database.insert() 用于向数据表中插入数据
database.insert("user", null, ["username": "ZhangSan", "password": "123456"])
// Database.query() 用于查询数据库内容
def data = database.query { table("user") }
$assert.assertTrue(data.length() == 1, "数据大小为1")
def user = data.get(0)
$assert.assertTrue(user.get("username") == "ZhangSan", "用户名")
$assert.assertTrue(user.get("password") == "123456", "密码")
// Databases.dropDatabase() 用于删除数据库
$assert.assertTrue($databases.dropDatabase(database), "删除数据库")
// 由于数据库已经删除,所以第二次调用会返回false
$assert.assertFalse($databases.dropDatabase("M8Test_test.db"), "第二次删除数据库")
```