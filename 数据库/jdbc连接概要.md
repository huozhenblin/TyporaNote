## **1. JDBC体系结构**

JDBC接口（API）包括两个层次：

**面向应用的API**：Java API，抽象接口，供应用程序开发人员使用（连接数据库，执行SQL语句，获得结果）。

**面向数据库的API**：Java Driver API，供开发商开发数据库驱动程序用。

**JDBC是sun公司提供一套用于数据库操作的接口，java程序员只需要面向这套接口编程即可。**不同的数据库厂商，需要针对这套接口，提供不同实现。不同的实现的集合，即为不同数据库的驱动。 ————面向接口编程**

## **2. JDBC程序编写步骤**

![image-20200421175900822](D:\my\study\TyporaNote\数据库\images\image-20200421175900822.png)

补充：ODBC(**Open Database Connectivity**，开放式数据库连接)，是微软在Windows平台下推出的。使用者在程序中只需要调用ODBC API，由 ODBC 驱动程序将调用转换成为对特定的数据库的调用请求。

## **3.获取数据库连接**

### **Driver接口实现类**

java.sql.Driver 接口是所有 JDBC 驱动程序需要实现的接口。这个接口是提供给数据库厂商使用的，不同数据库厂商提供不同的实现。

在程序中不需要直接去访问实现了 Driver 接口的类，而是由驱动程序管理器类(java.sql.DriverManager)去调用这些Driver实现。

Oracle的驱动：**oracle.jdbc.driver.OracleDriver**

mySql的驱动： **com.mysql.jdbc.Driver**

### **URL**

JDBC URL的标准由三部分组成，各部分间用冒号分隔。

**jdbc:子协议:子名称**

协议**：JDBC URL中的协议总是jdbc**

子协议**：子协议用于标识一个数据库驱动程序**

子名称**：一种标识数据库的方法。子名称可以依不同的子协议而变化，用子名称的目的是为了**定位数据库**提供足够的信息。包含**

主机名**(对应服务端的ip地址)**，端口号，数据库名**

![image-20200421180243139](D:\my\study\TyporaNote\数据库\images\image-20200421180243139.png)

### **用户名和密码**

user,password可以用“属性名=属性值”方式告诉数据库可以调用 DriverManager 类的 getConnection() 方法建立到数据库的连接

## 4.**数据库连接方式举例**

### 方式一

~~~java
@Test
public void testConnection1() {
try {
//1.提供java.sql.Driver接口实现类的对象
Driver driver = null;
driver = new com.mysql.jdbc.Driver();

//2.提供url，指明具体操作的数据
String url = "jdbc:mysql://localhost:3306/test";

//3.提供Properties的对象，指明用户名和密码
Properties info = new Properties();
info.setProperty("user", "root");
info.setProperty("password", "abc123");

//4.调用driver的connect()，获取连接
Connection conn = driver.connect(url, info);
System.out.println(conn);
} catch (SQLException e) {
e.printStackTrace();
}
}
~~~

### **方式二**

说明：相较于方式一，这里使用反射实例化Driver，不在代码中体现第三方数据库的API。体现了面向接口编程思想。

~~~java
@Test
public void testConnection2() {
try {
//1.实例化Driver
String className = "com.mysql.jdbc.Driver";
Class clazz = Class.forName(className);
Driver driver = (Driver) clazz.newInstance();

//2.提供url，指明具体操作的数据
String url = "jdbc:mysql://localhost:3306/test";

//3.提供Properties的对象，指明用户名和密码
Properties info = new Properties();
info.setProperty("user", "root");
info.setProperty("password", "abc123");

//4.调用driver的connect()，获取连接
Connection conn = driver.connect(url, info);
System.out.println(conn);

} catch (Exception e) {
e.printStackTrace();
}
}
~~~

### **方式三**

~~~java
@Test
public void testConnection3() {
try {
//1.数据库连接的4个基本要素：
String url = "jdbc:mysql://localhost:3306/test";
String user = "root";
String password = "abc123";
String driverName = "com.mysql.jdbc.Driver";

//2.实例化Driver
Class clazz = Class.forName(driverName);
Driver driver = (Driver) clazz.newInstance();
//3.注册驱动
DriverManager.registerDriver(driver);
//4.获取连接
Connection conn = DriverManager.getConnection(url, user, password);
System.out.println(conn);
} catch (Exception e) {
e.printStackTrace();
}
}
~~~

### **方式四**

说明：不必显式的注册驱动了。因为在DriverManager的源码中已经存在静态代码块，实现了驱动的注册。

~~~java
@Test
public void testConnection4() {
try {
//1.数据库连接的4个基本要素：
String url = "jdbc:mysql://localhost:3306/test";
String user = "root";
String password = "abc123";
String driverName = "com.mysql.jdbc.Driver";

//2.加载驱动 （①实例化Driver ②注册驱动）
Class.forName(driverName);


//Driver driver = (Driver) clazz.newInstance();
//3.注册驱动
//DriverManager.registerDriver(driver);
/*
可以注释掉上述代码的原因，是因为在mysql的Driver类中声明有：
static {
try {
DriverManager.registerDriver(new Driver());
} catch (SQLException var1) {
throw new RuntimeException("Can't register driver!");
}
}

*/

//3.获取连接
Connection conn = DriverManager.getConnection(url, user, password);
System.out.println(conn);
} catch (Exception e) {
e.printStackTrace();
}

}
~~~

### **方式五(最终版)**

~~~java
@Test
public void testConnection5() throws Exception {
//1.加载配置文件
InputStream is = ConnectionTest.class.getClassLoader().getResourceAsStream("jdbc.properties");
Properties pros = new Properties();
pros.load(is);

//2.读取配置信息
String user = pros.getProperty("user");
String password = pros.getProperty("password");
String url = pros.getProperty("url");
String driverClass = pros.getProperty("driverClass");

//3.加载驱动
Class.forName(driverClass);

//4.获取连接
Connection conn = DriverManager.getConnection(url,user,password);
System.out.println(conn);

}
~~~

其中，配置文件声明在工程的src目录下：【jdbc.properties】

~~~properitites
user=root
password=abc123
url=jdbc:mysql://localhost:3306/test
driverClass=com.mysql.jdbc.Driver
~~~

