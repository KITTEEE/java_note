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



