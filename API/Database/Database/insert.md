功能:

+ 向数据表中插入数据

定义:

+ Long insert(String table, String nullColumnHack, Map<String, Object> values)

参数:

+ String table - 表名
+ String nullColumnHack -
  当values参数为空或者里面没有内容的时候，我们insert是会失败的（底层数据库不允许插入一个空行），为了防止这种情况，我们要在这里指定一个列名，到时候如果发现将要插入的行为空行时，就会将你指定的这个列名的值设为null，然后再向数据库中插入
+ Map<String, Object> values - 需要插入的数据,键值对形式,键为列名,值为需要插入的值

返回值:

+ Long - 新插入行的行ID，如果发生错误，则为-1

示例代码:

+ 通过 [Database.insert()](/API/Database/Database/README.md?id=insert) 向数据表中插入数据

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Databases.openOrCreateDatabase() 用于打开/创建数据库
def database = $databases.openOrCreateDatabase("M8Test_test.db")
// Database.createTable() 用于新建一个简单数据表,该表所有列均为text类型,并且存在自增id属性
database.createTable("user", ["username", "password"])
// Database.insert() 用于向数据表中插入数据
$assert.assertTrue(database.insert("user", null, ["username": "ZhangSan", "password": "123456"]) == 1, "插入行ID为1")
// Database.query() 用于查询数据库内容
def data = database.query { table("user") }
$assert.assertTrue(data.length() == 1, "数据大小为1")
def user = data.get(0)
$assert.assertTrue(user.get("username") == "ZhangSan", "用户名")
$assert.assertTrue(user.get("password") == "123456", "密码")
// Databases.dropDatabase() 用于删除数据库
$assert.assertTrue($databases.dropDatabase(database), "删除数据库")
```