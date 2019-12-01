
## commons

### StringExtUtils

- 驼峰转下划线

``` java
StringExtUtils.toUnderscore("HelloWorld");  // => "hello_world"
StringExtUtils.toUnderscore("helloWorld");   // =>  "hello_world"
StringExtUtils.toUnderscore("Hello2World");  // =>  "hello2_world"
StringExtUtils.toUnderscore("HElloWOrld");   // => "h_ello_w_orld"
```

- 下划线转驼峰

``` java
StringExtUtils.toCamel("hello_world");  // => "helloWorld"
StringExtUtils.toCamel("HELLO_WORLD");  // => "helloWorld"
StringExtUtils.toCamel("Hello_WoRld");  // => "helloWorld"
```

- 下划线转帕斯卡

``` java
StringExtUtils.toPascal("hello_world");  // => HelloWorld
StringExtUtils.toPascal("HELLO_WORLD");  // => HelloWorld
StringExtUtils.toPascal("Hello_WoRld");  // => HelloWorld
```

- 分隔大写字符

``` java
StringExtUtils.uppercaseSeparate("HelloWorld", "-");  // => "hello-world"
StringExtUtils.uppercaseSeparate("helloWorld", "@");  // => "hello@world"
```

- 获取第一个切割点之后的文本

``` java
StringExtUtils.subStringFirstAfter("abcdef", "c");  // => def
StringExtUtils.subStringFirstAfter("abcdef", "g");  // => abcdef
StringExtUtils.subStringFirstAfter("abcdefabcdef", "c");  // => defabcdef
```

### RandomStringExtUtils

- 随机生成中文字符

``` java
RandomStringExtUtils.randomChinese(5); // => 已很结同总
```

- 随机生成常用中文字符（包括复杂字符）

``` java
// 随机生成3到5个中文字符
RandomStringExtUtils.randomFrequentlyUsedChinese(3,5); // => 耆牮俤畸蹬
```

- 随机生成姓名

``` java
RandomStringExtUtils.randomName();  // => 虞任
```

- 列表中随机取值

``` java
String name = RandomStringExtUtils.randomFromList("张三", "李四", "王五", "赵六");  
int i = RandomStringExtUtils.randomFromList(1,7,9,10);  // => 

```

### ArrayExtUtils

- 分割为指定长度的列表

``` java
String[] data = new String[]{"1000000008334", "1000000008333", "1000000008332", "1000000008331", "1000000008330", "1000000008329", "1000000008328"};
List<String[]> result = ArrayExtUtils.split(data, 2);
```

### DateExtUtils

- 随机生成日期

``` java
 Date randomDate = DateExtUtils.random();
```

- 随机生成指定范围内的日期

``` java
Calendar startDate = Calendar.getInstance();
startDate.set(2009, 10, 10);

Calendar endDate = Calendar.getInstance();
endDate.set(2019, 10, 10);
        
Date randomDate = DateExtUtils.random(startDate.getTime(), endDate.getTime());
```

- 获取指定月份的第一天

``` java
Calendar calendar = Calendar.getInstance();
calendar.set(2019, 2, 1, 0, 0, 0); // 月份值要减1
calendar.set(Calendar.MILLISECOND, 0);

Date firstDayOfMonth = DateExtUtils.getFirstDayOfMonth("2019-03", "yyyy-MM");
Assert.assertEquals(calendar.getTime().getTime(), firstDayOfMonth.getTime());
```

- 获取指定月份的最后一天

``` java
Calendar calendar = Calendar.getInstance();
calendar.set(2019, 2, 31, 0, 0, 0); // 月份值要减1
calendar.set(Calendar.MILLISECOND, 0);

Date lastDayOfMonth = DateExtUtils.getLastDayOfMonth("2019-03", "yyyy-MM");
Assert.assertEquals(calendar.getTime().getTime(), lastDayOfMonth.getTime());
```

- 判断指定日期是否在某个区间范围内

``` java
Calendar calendar = Calendar.getInstance();
calendar.set(2019, 3, 20);

Calendar startDateCalendar = Calendar.getInstance();
startDateCalendar.set(2019, 3, 1);

Calendar endDateCalendar = Calendar.getInstance();
endDateCalendar.set(2019, 3, 31);
boolean dayBetween = DateExtUtils
                .isDayBetween(calendar.getTime(), startDateCalendar.getTime(), endDateCalendar.getTime());
```

### ListExtUtils

- 提取列表对象中某个字段的值，并拼接成字符串

``` java
List<User> users = new ArrayList<>();
for (int i = 0; i < 10; i++) {
    User user = new User();
    user.setId(i);
    user.setName("zhangsan" + i);
    users.add(user);
}
String ids = ListExtUtils.joinFieldValue(users, "id", "#");  // => 0#1#2#3#4#5#6#7#8#9
String ids2 = ListExtUtils.joinFieldValue(users, "id");  // => 0,1,2,3,4,5,6,7,8,9
```

- 判断对象集合中是否包含某个元素

``` java
List < User > users = new ArrayList < > ();
for (int i = 0; i < 10; i++) {
    User user = new User();
    user.setId(i);
    user.setName("zhangsan" + i);
    users.add(user);
}
Map < String, Object > kvMap = new HashMap() {
    {
        put("id", 3);
        put("name", "zhangsan3");
    }
};
// 存在
Assert.assertTrue(ListExtUtils.contains(users, kvMap));
Map < String, Object > kvMap2 = new HashMap() {
    {
        put("id", "3"); //类型不一致
    }
};
// 类型不一致，不存在
Assert.assertFalse(ListExtUtils.contains(users, kvMap2));

// 单字段匹配
Assert.assertTrue(ListExtUtils.contains(users, "id", 3));
```

- 对象集合中查找匹配的元素
- 对象集合中查找匹配的第一个元素

``` java
List < User > users = new ArrayList < > ();
for (int i = 0; i < 10; i++) {
    User user = new User();
    user.setId(i);
    user.setName("zhangsan" + i);
    users.add(user);
}
Map < String, Object > kvMap = new HashMap() {
    {
        put("id", 3);
        put("name", "zhangsan3");
    }
};
// 返回所有匹配的元素
List < User > findedUsers = ListExtUtils.find(users, kvMap);
Assert.assertEquals(findedUsers.toString(), "[User{id=3, name='zhangsan3', sex='null', age=null, birthDate=null}]");
// 返回第一个匹配的元素
User findedUser = ListExtUtils.findFirst(users, kvMap);
Assert.assertEquals(findedUser.toString(), "User{id=3, name='zhangsan3', sex='null', age=null, birthDate=null}");
```

### SerializationExtUtils

- 序列化对象（Object -> 十六进制字符串）

``` java
User user = new User();
user.setName("张三");
user.setId(1);
user.setBirthDate(new Date(2019, 10, 10));
user.setAge(20);

// 序列化
String serializedHexString = SerializationExtUtils.serialize(user);  // => aced000573720024636e2e6368656e7a772e746f6f6c6b69742e646f6d61696e2e656e746974792e55736572983a612a7abc9f590200054c00036167657400134c6a6176612f6c616e672f496e74656765723b4c00096269727468446174657400104c6a6176612f7574696c2f446174653b4c0002696471007e00014c00046e616d657400124c6a6176612f6c616e672f537472696e673b4c000373657871007e00037870737200116a6176612e6c616e672e496e746567657212e2a0a4f781873802000149000576616c7565787200106a6176612e6c616e672e4e756d62657286ac951d0b94e08b0200007870000000147372000e6a6176612e7574696c2e44617465686a81014b59741903000078707708000037f668c4a400787371007e000500000001740006e5bca0e4b88970

```

- 反序列化对象（十六进制字符串 -> Object）

``` java
User deserializeUser = SerializationExtUtils.deserialize(serializedHexString); // => User{id=1, name='张三', sex='null', age=20, birthDate=Mon Nov 10 00:00:00 CST 3919}

```

### ColorUtils

- 将十六进制颜色转RGB格式

``` java
Color color = ColorUtils.hexToRgb("70AD47");
// Color color = ColorUtils.hexToRgb("#70AD47");

Assert.assertEquals(color.getRed(), 112);
Assert.assertEquals(color.getGreen(), 173);
Assert.assertEquals(color.getBlue(), 71);
```

- 生成随机颜色

``` java
Color color = ColorUtils.randomColor(0, 255);
```

### RegexUtils

正则匹配工具类

- 是否IP地址
  - 是否IPv4
  - 是否IPv6

``` java
Assert.assertTrue(RegexUtils.isIPv4("10.2.2.4"));
Assert.assertTrue(RegexUtils.isIPv4("192.168.255.255"));

Assert.assertFalse(RegexUtils.isIPv4("1.1.1.1/12"));
Assert.assertFalse(RegexUtils.isIPv4("1.1.1"));
```

- 是否邮箱地址

``` java
Assert.assertTrue(RegexUtils.isEmail("656469722@qq.com"));
Assert.assertTrue(RegexUtils.isEmail("chenzw_123@16.com"));

// 非法字符串"#@"
Assert.assertFalse(RegexUtils.isEmail("chenzw#123@163.com"));
Assert.assertFalse(RegexUtils.isEmail("chenzw@123@163.com"));
```
- 是否QQ号码

``` java

```

- 是否身份证号码

``` java

```

- 是否手机号码

``` java

```

- 中文字符匹配
  - 是否包含中文
  - 是否全是中文
  
``` java

```

- 数值
  - 是否整数
  - 是否数字（整数和小数）
  
``` java

```

### ProjectUtils

项目相关工具类

- 获取项目根地址

``` java
ProjectUtils.getRootPath(); // => C:\Users\chenzw\IdeaProjects\toolkit
```

- 获取项目classpath地址

``` java
ProjectUtils.getClassPath(); // => /C:/Users/chenzw/IdeaProjects/toolkit/target/test-classes/
```

- 获取依赖jar列表

``` java
ProjectUtils.getDependentJarFiles();  // => jar文件列表
```

### FileExtUtils

文件工具类

- 获取两个路径的相对路径地址

``` java

```

### ClassExtUtils

- 判断某个类是否存在

``` java
 boolean present = ClassExtUtils.isPresent("cn.chenzw.toolkit.commons.DateExtUtils");  // => true
```

- 实例化对象

``` java
 Class<?> aClass = ClassExtUtils.forName("cn.chenzw.toolkit.commons.DateExtUtils"); // => Class对象
```

- 查找类所在Jar包

``` java
 URL sourceJar = ClassExtUtils.findSourceJar(DateUtils.class);  // => file:/C:/Users/yunli/.m2/repository/org/apache/commons/commons-lang3/3.9/commons-lang3-3.9.jar
```

### GenericUtils

泛型类工具

- 获取泛型参数

``` java

```

### BinaryConvertUtils

- bytes数组<=>十六进制字符串

``` java
BinaryConvertUtils.bytesToHexString("hello".getBytes());  // => 68656c6c6f
byte[] bytes = BinaryConvertUtils.hexStringToBytes("68656c6c6f"); // => hello
```

### UriExtUtils

uri操作工具类

- 添加参数

``` java
Map<String, String> params = new HashMap<>();
params.put("a", "111");
params.put("b", "222");

String uri = UriExtUtils.buildParams("http://www.baidu.com", params);  // => http://www.baidu.com?a=111&b=222

String uri2 = UriExtUtils.buildParams("http://www.baidu.com?k=1", params);  // => http://www.baidu.com?k=1&a=111&b=222

```

- 解析并获取uri参数

``` java
Map<String, String> uriParams = UriExtUtils.getUriParams(
                "http://192.168.17.231:8680/login?client_id=1&redirect_uri=http%3A%2F%2Fwww.baidu.com&authentication_type=oauth");  // => {redirect_uri=http%3A%2F%2Fwww.baidu.com, authentication_type=oauth, client_id=1}

```

### ZipUtils

压缩工具

- 压缩文件

``` java
try (OutputStream os = new FileOutputStream(new File("src.zip"))) {
    ZipUtils.toZip(new File("src"), os);
}
```
