## Java 的常用 API

### Object 类

Object 类是所有类的父类，它描述的所有方法子类都可以使用，所有类在创建对象的时候，最终找的父类就是Object。

#### equals 方法

equals 比较的是两个对象是否相同（由于对象是引用数据类型，比较的是两个对象的内存地址），equals 方法通常用来比较两个对象中的属性值（需要子类重写）。

```java
class Person extends Object {
    int age;
    public boolean equals(Object obj) {
        if(this==obj) {
            return true;
        }
        if(obj instanceof Person) {
            Person p = (Person)obj;
            return this.age == p.age;
        }return false;
    }
}
```

注：由于 equals 方法的参数是 object 类型，在调用对象属性时一定要进行类型转换，且在转换前须进行类型判断。



### toString 方法

toString方法返回该对象的字符串表示（就是内存地址）。

由于toString方法返回的结果是内存地址，而在开发中，经常需要按照对象的属性得到相应的字符串表现形式，因此也需要重写它。



### String 类

字符串是常量，他们的值在创建后不可变，但 string 对象中记录的地址值(指向)是可变的。



#### String 类构造方法

```java
String s1 = new String(); //创建String对象，字符串中没有内容

byte[] bys = new byte[]{97,98,99,100};
String s2 = new String(bys); // 创建String对象，把数组元素作为字符串的内容
String s3 = new String(bys, 1, 3); //创建String对象，把一部分数组元素作为字符串的内容，参数offset为数组元素的起始索引位置，参数length为要几个元素
	
char[] chs = new char[]{’a’,’b’,’c’,’d’,’e’};
String s4 = new String(chs); //创建String对象，把数组元素作为字符串的内容
String s5 = new String(chs, 0, 3);//创建String对象，把一部分数组元素作为字符串的内容，参数offset为数组元素的起始索引位置，参数count为要几个元素
String s6 = new String(“abc”); //创建String对象，字符串内容为abc
```



#### String 类的方法查找

```java
int length()//返回字符串长度
//返回一个新字符串，内容为指定位置开始到字符串末尾的所有字符
String substring(int beginIndex)
//返回一个新字符串，内容为指定位置开始到指定位置结束所有字符
String substring(int beginIndex,int endIndex)
//测试此字符串是否以指定的前缀开始或结束
boolean startWith(String prifix)
boolean endWith(String suffix)
//当且仅当此字符串包含指定的 char 值序列时，返回 true
boolean contains(CharSequence s)
//返回指定字符串第一次出现的索引,不包含返回-1
int indexOf(String str)
//将字符串转成一个字符数组或字节数组
byte[] getBytes()//使用默认字符集将 String 编码为 byte 序列，并将结果存储到一个 byte 数组中
char[] toCharArray()//将此字符串转换为一个新的字符数组
//判断连个字符串内容是否相同
boolean equals(Object object)
boolean equalsIgnoreCase(String anotherString)//忽略大小写
```



### StringBuffer 类

字符缓冲区类是一个容器，可以装很多字符串，并对其中的字符串进行操作，**支持可变的字符串(与 String 区别)**。



#### StringBuffer 的方法

```java
StringBuffer append(String str)//将指定字符串追加到此字符序列
StringBuffer delete(int start,int end)//移除指定索引的字符
StringBuffer insert(int offset,String str)//将字符串插入到指定索引位置
StringBuffer reverse()//字符串反转
```



#### 对象的方法链式调用

开发中会遇到调用一个方法后，返回一个对象的情况。然后使用返回的对象继续调用方法。

```java
StringBuffer sb = new StringBuffer();
String str = sb.append(true).append("hehe").toString();
```



#### StringBuilder 类

StringBuilder 类被设计用作 StringBuffer 的一个简易替换，用在字符串缓冲区被单个线程使用的时候，大多数实现中比 StringBuffer 更快，但 StringBuffer 更为安全。



### 正则表达式

#### 正则表达式匹配规则

* 字符 x ：代表某个字符，如匹配规则为 "a" ，那么需要匹配的字符串内容就是 "a" 。

* 字符 \\\ :  第一个斜杠表示转义，总体代表 ‘ \ ’

* 字符 \\t ：代表制表符

* 字符 \\n：代表换行

* 字符类 [abc] ：代表需要匹配的内容是字符 a、b、或 c 中的一个。

* 字符类 **[^abc]** : 代表除了 a b c 以外的任意字符

* 字符类 [a-zA-z]：代表的是需要匹配的是一个大写或者小写的字母

* 字符类 [0-9] ：代表的需要匹配一个在 0 到 9 中的一个数字。

* 字符类 [a-zA-z_0-9]：代表需要匹配的是一个字母或数字或一个下划线

* 预定义字符类 .  ：代表的是需要匹配一个任意字符，如果就想使用 . 的话，需要使用匹配规则 "\\\\." 来实现。

* 预定义字符类 \\d ：相当于 [0-9] 

* 预定义字符类 \\w：相当于 [a-zA-z_0-9]

*   **边界匹配器：^** 代表的是行的开头

  例如：匹配规则为**^[abc][0-9]$** ，那么需要匹配的内容从[abc]这个位置开始, 相当于左双引号 

  **边界匹配器：$** 含义：代表的是行的结尾

  例如：匹配规则为**^[abc][0-9]$** ，那么需要匹配的内容以[0-9]这个结束, 相当于右双引号 

  **边界匹配器：\b** 含义：代表的是单词边界

  例如：匹配规则为**"\b[abc]\b"** ，那么代表的是字母a或b或c的左右两边需要的是非单词字符(**[a-zA-Z_0-9]**)

* 数量词 : x?   表示 x 出现一次或一次也没有
* 数量词：x* 表示 x 出现零次或多次
* 数量词：x+ 表示 x 出现一次或多次
* 数量词：X{n}  代表的是X出现恰好 n 次，例如：匹配规则为**"a{5}"**，那么需要匹配的内容是5个字符a
* 数量词：X{n,} 代表的是X出现至少 n 次，例如：匹配规则为**"a{5, }"**，那么需要匹配的内容是最少有5个字符a
* 数量词：X{n,m} 代表的是X出现至少 n 次，但是不超过 m 次，例如：匹配规则为 **"a{5,8}"**，那么需要匹配的内容是有 5 个字符 a 到 8 个字符 a 之间



#### Java 中正则表达式的常用方法

```java
boolean matches(String regex)//判断是否匹配给定的规则
String qq = "02345";
String regex = "[1-9][0-9]{4,14}";
boolean flag = qq.matches(regex);
System.out.println(flag);

String[] split(String regex)//根据给定正则表达式的匹配规则拆分字符串
String str = "18.22.40.65";
String regex = "\\.";
String[] result = str.split(regex);
for(int i = 0; i < result.length; i++) {
	System.out.println(result[i]);
}

String replaceAll(String regex,String replacement)//将符合规则的字符串替换为新的字符串
String string = "Hello12345World6789012";
String regex = "[0-9]";
String result = string.replaceAll(regex, "*");
System.out.println(result);
```



#### 常用匹配

* 匹配正确数字

  匹配正整数：”\\d+”

  匹配正小数：”\\d+\\.\\d+”  

  匹配负整数：”-\\d+”

  匹配负小数：”-\\d+\\.\\d+”

  匹配保留两位小数的正数：”\\d+\\.\\d{2}”

  匹配保留1-3位小数的正数：”\\d+\\.\\d{1,3}”

* 匹配邮箱 ： ”[a-zA-Z_0-9]+@[a-zA-Z_0-9]+(\\.[a-zA-Z_0-9]+)+”



### Date 类

#### Date 类的两个构造函数

```java
Date()获取系统当前时间并分配给对象，精确到毫秒
Date(long date)long date 表示毫秒数，能得到从时间原点开始到毫秒数的时间
//时间原点：1970 年 1 月 1 日 00：00：00 GMT
Date date = new Date(1607616000000L);
System.out.println(date);
//打印结果：Fri Dec 11 00:00:00 CST 2020

long getTime() 方法
返回从时间原点以来的 Date 对象的毫秒数
```



### DateFormat类

DateFormat 类常用于完成日期和文本之间的转换，DateFormat 是抽象类，在使用时需要其子类 SimpleDateFormat 来创建对象。

```java
//SimpleDateFormat 类的规则说明：
当出现y时，会将y替换成年
当出现M时，会将M替换成月
当出现d时，会将d替换成日
当出现H时，会将H替换成时
当出现m时，会将m替换成分
当出现s时，会将s替换成秒
```

#### DateFormat 常用 方法

```java
String format(Date date) 将一个 Date 对象转化为 String
Date parse(String source) 用来将String 转换成 Date，转换时 String 要符合格式

//将 Date 对象 转换为 String
DateFormat df = new SimpleDateFormat("yyyy-MM-dd");
Date date = new Date();
String str = df.format(date);//2019年3月19日

//将 String 对象转换为 Date 
String string = "2019年3月8日";
DateFormat dateFormat = new SimpleDateFormat("yyyy年MM月dd日");
Date date = dateFormat.parse(string);
System.out.println(date);
```



### Calendar类

日历类 Calendar 替换了许多 Date 方法，它是一个抽象类，在创建对象时通过静态方法创建而非直接创建。

```java
//创建 Calendar 类
Calendar c = Calendar.getInstance();
```



#### Calendar 类常用方法

```java
public int get(int field) //获取时间字段
//MONTH 月（从0算起，最大11，0 表 1 月，11 表 12 月） DATE 天 HOUR 时
public void add(int field,int amount)//指定字段增加某值
public final void set(int field,int value)//设置指定字段的值
public final Date getTime()//获取该日历对象转成的日期对象
//示例    
Calendar calendar = Calendar.getInstance();
calendar.add(Calendar.YEAR, 3);
int year = calendar.get(Calendar.YEAR);
System.out.println(year);//2022
calendar.set(Calendar.YEAR,2019);
System.out.println(year2);//2019
Date d = calendar.getTime();
System.out.println(date);//Tue Mar 19 13:11:34 CST 2019
```

注意：

* 西方星期的开始为周日，中国为周一。

* 在Calendar类中，月份的表示是以0-11代表1-12月。

* 日期是有大小关系的，时间靠后，时间越大。