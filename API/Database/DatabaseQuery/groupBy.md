功能:

+ 设置分组

定义:

+ [DatabaseQuery](/API/Database/DatabaseQuery/README.md) groupBy(String groupBy)

参数:

+ String groupBy - 分组条件

返回值:

+ [DatabaseQuery](/API/Database/DatabaseQuery/README.md) - 返回对象本身,方便链式调用

示例代码:

+ 通过 [DatabaseQuery.groupBy()](/API/Database/DatabaseQuery/README.md?id=groupBy) 设置分组

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Databases.openOrCreateDatabase() 用于打开/创建数据库
def database = $databases.openOrCreateDatabase("M8Test_test.db")
// Database.createTable() 用于新建一个简单数据表,该表所有列均为text类型,并且存在自增id属性
database.createTable("user", ["username", "password", "city"])
// Database.insert() 用于向数据表中插入数据
database.insert("user", null, ["username": "ZhangSan", "password": "123456", "city": "广州"])
database.insert("user", null, ["username": "LiSi", "password": "123456", "city": "北京"])
database.insert("user", null, ["username": "WangWu", "password": "123456", "city": "广州"])
// Database.query() 用于查询数据库内容
def data = database.query {
    // delegate -> DatabaseQuery
    // DatabaseQuery.table() 用于设置需要查询的表名
    table("user")
    // DatabaseQuery.columns() 用于设置查询返回的列
    columns(["city", "count(*) as population"])
    // DatabaseQuery.groupBy() 用于设置分组
    groupBy("city")
}
$assert.assertTrue(data.length() == 2, "数据大小为2")
def user = data.get(0)
$assert.assertTrue(user.get("city") == "北京", "北京")
$assert.assertTrue(user.getInt("population") == 1, "北京人口")
user = data.get(1)
$assert.assertTrue(user.get("city") == "广州", "广州")
$assert.assertTrue(user.getInt("population") == 2, "广州人口")
// Databases.dropDatabase() 用于删除数据库
$assert.assertTrue($databases.dropDatabase(database), "删除数据库")
```