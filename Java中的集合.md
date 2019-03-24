## Java中的集合

### 集合

集合是 java 中的一种容器，用来存储多个数据。数组也是一种存放数据的容器，它们的区别在于：1. 数组的长度固定，而集合的长度可变。2. 集合中存储的元素必须是引用数据类型数据。



#### 集合中的继承关系

Collection 接口为集合中最顶层的接口，Collection 中常用的接口有  List 和 Set 接口。

List 接口中常用的子类有 ArrayList 、LinkedList 类。

Set 接口中常用的子类有 HashSet类、LinkedHashSet 类。



#### 使用集合时注意

* 集合中存储的其实都是对象地址
* jdk1.5 之后可以存储基本数值，因为出现了包装类，提供了自动装箱操作，所以集合中的元素就是基本数值的包装类对象



### Collection 接口

### Collection 接口中的方法

```java
Object[] toArray() //方法返回一个存储对象的数组
boolean contains(Object o)//判断对象是否存在于集合中，返回一个 boolean 值
void clear() //清空集合中的所有元素,但集合本身依然存在
boolean remove(Object o)//移除集合中指定的元素
public static void main (String[] args){
	function_1();    
}
public static void function_1(){
    Collection<String> coll = new ArrayList<String>();
    coll.add("heihei");
    coll.add("haha");
    coll.add("xixi");
    coll.add("123");
    Object[] objs = coll.toArray();
    for(int i = 0 ; i < objs.length; i++) {
        Syso(objs[i]);
    }
    boolean b1 = coll.contains("haha");//true
    boolean b2 = coll.remove("123");//true
    Syso(coll);
    coll.clear;
    Syso(coll);
}
```



### Iterator 迭代器

java 中提供的集合不止 Collection 一种，且不同集合在存储元素时采用的存储方式也不同，要获取这些不同集合中的元素，就需要有一种通用的获取方式，**Iterator 迭代器就是获取集合元素的一种通用方式。**

获取 Collection 集合中的元素都需要在取元素前判断集合是否有元素，如果有，就取出，然后继续判断，直到所有元素全部取出，这种取出方式被称为迭代。**Iterator 迭代器定义了统一的判断元素和取元素方法。**



#### Iterator实现

```java
public static void main(String args[]) {
    Collection<String> coll = new ArrayList()<String>;
    coll.add("abc1");
    coll.add("abc2");
    coll.add("abc3");
    coll.add("abc4");
    Iterator it = coll.iterator();//调用集合的方法 iterator() 获取 Iterator接口的实现类对象
    while(it.hasNext()){
        String s = it.next();
        Syso(s);
    }
}
```



#### Iterator 实现原理

```java
//hasNext()
//cursor记录的索引值不等于集合的长度返回true,否则返回false
public boolean hasNext() {       
	return cursor != size; //cursor初值为0                 
}
//next()
//①返回cursor指向的当前元素 
//②cursor++
public Object next() {            
	int i = cursor; 
	cursor = i + 1;  
	return  elementData[lastRet = i];      
}
```



#### Iterator 中的转型

```java
Collection coll = new ArrayList();//没有使用泛型决定元素类型，所以存储时提升了 Object
coll.add('abc');
Iterator it = coll.iterator();
while(it.hasNext()) {
    //由于元素被存放进集合后全部被提升为Object类型
 	//当需要使用子类对象特有方法时，需要向下转型
    //注意：如果集合中存放的是多个对象，这时进行向下转型会发生类型转换异常。
    String str = (String)it.next();
}
```



### 增强 for 循环

格式：

```java
for(数据类型  变量名 : 数组或者集合){
	sop(变量);
}
```



#### 增强 for 的好处和弊端

好处: 代码少了,方便对容器遍历。

弊端: 没有索引,不能操作容器里面的元素。

```java
public static void function(){
    int[] arr = {3,1,9,0};
    for(int i : arr){
      System.out.println(i+1);// 4  2  10  1
    }
    System.out.println(arr[0]);// 3
  }
```



#### 增强 for 循环遍历集合

```java
ArrayList<Person> al = new ArrayList<Person>();
	al.add(new Person("a",20));
	al.add(new Person("b", 21));
	for(Person p : al){
		System.out.println(p.getName());
		System.out.println(p.toString());//需重写toString()方法
	}
```



### 泛型

#### java 中的伪泛型

泛型只在编译时存在，编译后就被擦除，在编译之前我们就可以限制集合的类型，起到作用。
例如:ArrayList<String> al=new ArrayList<String>();
编译后:ArrayList al=new ArrayList();



#### 泛型的好处

* 将运行时期的 ClassCastException 转移到了编译时期的编译失败

* 避免了类型强转的麻烦

  

#### 泛型的通配符

泛型的通配，匹配所有的数据类型 ？

```java
//定义方法可同时迭代两种不同的集合
public static void main(String[] args) {
    ArrayList<String> array = new ArrayList<String>();
    HashSet<Integer> set = new HashSet<Integer>();
    array.add("123");
    array.add("456");
    set.add(789);
    set.add(890);
    iterator(array);
    iterator(set);
}
public static void iterator(Collection<?> coll){
	Iterator<?> it = coll.iterator();
	while(it.hasNext()){
	//it.next()获取的对象,什么类型
	System.out.println(it.next());
	}
}
```



#### 泛型的限定

略



----------------



### List 接口

List 接口的特点

* **有序。** List 是一个元素存取有序的集合l  例如，存元素的顺序是11、22、33。那么集合中，元素的存储就是按照11、22、33的顺序完成的）。
* **带有索引。** 通过索引就可以精确的操作集合中的元素（与数组的索引是一个道理）。
* **允许有重复的元素。** 通过元素的equals方法，来比较是否为重复的元素。



#### List 接口中的常用方法

```java
* 增加元素
add(Object e) //向集合末尾添加指定元素
add(int index,Object e)//向集合指定索引处添加指定元素，原有元素依次后移
* 删除元素
remove(Object e) //删除指定元素对象，返回值为被删除的元素
remove(int index) //删除指定索引处的元素，返回值为被删除的元素
* 替换元素
set(int index,Object e) //将制定索引处的元素替换为指定元素，返回值为替换前的元素
* 查询元素
get(int index) //获取指定索引处的元素并返回
```

```java
//方法演示
List<String> list = new ArrayList<String>();
list.add("a");
list.add("b");
list.add("c");
list.add(1,"d") // [a,d,b,c]
list.remove(1) // [a,b,c] 返回值为 d
list.set(1,"d") // [a,d,c] 返回值为 b
Iterator<String> it = list.iterator();
//迭代过程中使用了集合的方法对集合进行操作，导致迭代器并不知道集合中的变化，容易引发数据的不确定性，通常会出现并发修改异常(java.util.ConcurrentModificationExcepiton)
while(it.hasNext()){
    String s = it.next();
    if("a".equals(s)){
        list.add("d");//该操作会导致程序出错
    }
}
```

由于List集合拥有索引，因此List集合迭代方式除了使用迭代器之外，还可以使用索引进行迭代。

并发修改异常解决办法：

* 在迭代时，不要使用集合的方法操作元素。

* 或者通过ListIterator迭代器操作元素是可以的，ListIterator的出现，解决了使用Iterator迭代过程中可能会发生的错误情况。



#### List 集合存储数据的结构

List接口下有很多个集合，它们存储元素所采用的结构方式是不同的，这样就导致了这些集合有它们各自的特点。

**ArrayList 集合**是数组结构，元素增删慢，查找快，日常开发中使用最多的功能为查询数据、遍历数据

**LinkedList 集合**是链表+栈结构，增删快，查找慢，实际开发中对一个集合元素的添加与删除经常涉及到首尾操作，而 LinkedList 提供了大量首尾操作的方法。

```java
//LinkedList 的特有方法
addFirst(E e) / addLast(E e) //将指定元素插入到列表的开头或结尾
getFirst() / getLast() // 返回链表的第一个或最后一个元素
removeFirst() / removeLast() //移除并返回列表的第一个或最后一个元素
pop()//从链表所表示的堆栈处弹出一个元素
push()//将元素推入链表所表示的堆栈
isEmpty()//如果链表为空，返回true
```



### Set接口

**Set 接口特点**

* 元素不重复
* 没有索引
* 无序集合

HashSet 类实现 Set 接口，由哈希表支持（实际上是一个 HashMap集合）。HashSet 集合不能保证的迭代顺序与元素存储顺序相同。

HashSet 集合，采用哈希表结构存储数据，保证元素唯一性的方式依赖于：hashCode()与equals()方法。

**HashSet 集合自身特点**：底层为哈希表，存取速度快，线程不安全，运行速度快



#### 哈希表

哈希表底层使用的也是数组机制，数组中也存放对象，而这些对象往数组中存放时的位置比较特殊，当需要把这些对象给数组中存放时，那么会根据这些对象的特有数据结合相应的算法，计算出这个对象在数组中的位置，然后把这个对象存放在数组中。而这样的数组就称为哈希数组，即就是哈希表。

#### **哈希表的存储过程**

每存入一个新的元素都要走三步：

* 首先调用本类的hashCode()方法算出哈希值

* 在容器中找是否与新元素哈希值相同的老元素，如果没有直接存入，如果有转到第三步。

* 新元素会与该索引位置下的老元素利用equals方法一一对比，一旦新元素.equals(老元素)返回true,停止对比,说明重复,不再存入。如果与该索引位置下的老元素都通过equals方法对比返回false,说明没有重复,存入。



#### HashSet 存储 JavaAPI 中的类型元素

给 HashSet 中存储 JavaAPI 中提供的类型元素时，不需要重写元素的 hashCode 和 equals 方法，因为这两个方法，在 JavaAPI 的每个类中已经重写完毕，如 String 类、Integer 类等。

```java
HashSet<String> hs = new HashSet<String>();
hs.add("张三");
hs.add("李四");
hs.add("王五");
Iterator<String> it = hs.iterator();
while(it.hasNext()){
    String s = it.next();
    Syso(s);
}
```



#### HashSet 存储自定义类型元素

给 HashSet 中存放自定义类型元素时，**需要重写对象中的 hashCode 和 equals 方法**，建立自己的比较方式，才能保证 HashSet 集合中的对象唯一。

```java
public class Student {
	private String name;
	private int age;
    public int hashCode(){
		final int prime = 31;
		int result = 1;
		result = prime * result + age;
		result = prime * result + ((name==null) ? 0:name.hashCode());
		return result;
	}
	public boolean equals(Object obj){
		if(this == obj){
			return true;
		}
		if(!(obj instanceof Student)){
			System.out.println("类型错误");
			return false;
		}
		Student other = (Student)obj;
		return this.age == other.age && this.name.equals(other.name);
	}
	public String toString(){
		return "Student [name=]" + name + ", age=" + age + "]";
	}
}

public static void main(String[] args) {
		HashSet hs = new HashSet();
		hs.add(new Student("zhangsan",21));
		hs.add(new Student("lisi",22));
		hs.add(new Student("wangwu",23));
		hs.add(new Student("zhangsan",21));
		Iterator it = hs.iterator();
		while(it.hasNext()){
			Student student = (Student)it.next();
			System.out.println(student);
		}
	}
```



#### LinkedHashSet 集合

LinkedHashSet 继承自 HashSet ，是基于链表的哈希表实现。

LinkedHashSet 特性：**有顺序，存取顺序相同，**线程不安全，运行速度快。

```java
public static void main(String[] args) {
	Set<String> set = new LinkedHashSet<String>();
	set.add("bbb");
	set.add("aaa");
	set.add("abc");
	set.add("bbc");
	Iterator it = set.iterator();
	while (it.hasNext()) {
		System.out.println(it.next());// bbb,aaa,abc,bbc
	}
}
```



#### 其他

**hashCode 和 equals 方法面试题** 

两个对象  Person  p1 p2

问题：如果两个对象的哈希值相同 p1.hashCode()==p2.hashCode()

两个对象的equals一定返回true吗  p1.equals(p2) 一定是true吗

正确答案：不一定，两个对象哈希值无论相同还是不同,equals都可能返回true。

问题：如果两个对象的equals方法返回true,p1.equals(p2)==true

两个对象的哈希值一定相同吗

正确答案: 一定，如果两个对象是相等的，那么对这两个对象中的每个对象调用 hashCode 方法都必须生成相同的整数结果。 



------



### Map 接口



#### Map 和 Collection 的区别

* Collection 接口的集合的采用一个个元素的方式存储，而 Map 接口的集合中每个元素成对存在，由键和值两部分组成，通过键可以找到所对应的值。
* Map 不能包含重复的键，但可以包含重复值，每个键只对应一个值。

**Map 的常用集合为 HashMap 和 LinkedHashMap 集合**

* **HashMap<K,V>**：存储数据采用的哈希表结构，元素的存取顺序不能保证一致。由于要保证键的唯一、不重复，需要重写键的 hashCode() 方法、equals() 方法。

* **LinkedHashMap<K,V>**：继承 HashMap ，存储数据采用的哈希表结构+链表结构。通过链表结构可以保证元素的存取顺序一致；通过哈希表结构可以保证的键的唯一、不重复，需要重写键的 hashCode() 方法、equals() 方法。



#### Map 接口常用方法

```java
V put(K key,V value)//将指定的键与值对应起来，并添加到集合中,返回值为键所对应的值
V get(Object key)//获取指定键所对应的值,如果不包含映射关系则返回null
V remove(Object key)//根据指定的键(key)删除元素，返回被删除元素的值(value)。
public static void main(String[] args) {
	Map<String, String> map = new HashMap<String,String>();
	map.put("星期一", "Monday");
	map.put("星期二", "Tuseday");
	System.out.println(map);
	//当给Map中添加元素，会返回key对应的原来的value值，若key没有对应的值，返回null
	System.out.println(map.put("星期一", "Mon")); // Monday
	System.out.println(map.put("星期三", "Wen")); // null
	//根据指定的key获取对应的value
	String en = map.get("星期一");
	System.out.println(en);//Mon
	//根据key删除元素,会返回key对应的value值
	String value = map.remove("星期一");
	System.out.println(value);//Mon
	System.out.println(map);
}

```



#### Map 集合遍历键找值

**遍历map集合：调用keySet将map集合中的所有键存储到set集合中，遍历set集合，获取出set集合中的所有元素，通过iterator或增强for调用map的get，通过键获取到值。**

```java
Set<K> keySet()
//示例
public static void main(String[] args) {
	Map<String, String> map = new HashMap<String,String>();
	map.put("邓超", "孙俪");
	map.put("李晨", "范冰冰");
	map.put("刘德华", "柳岩");
	//获取Map中的所有key
	Set<String> set = map.keySet();
	//遍历存放所有key的set集合
	Iterator<String> iterator = set.iterator();
	while(iterator.hasNext()){
		String key = iterator.next();
		String value = map.get(key);
		System.out.println(key + " = " + value);
	}
}
```



### Map 集合的Entry对象

Entry 是 Map 的一个内部接口，由Map的子类的内部类实现。

Entry将键值对的对应关系封装成了对象。这样在遍历Map集合时，就可以从每一个键值对（Entry）对象中获取对应的键与对应的值。

#### Entry常用方法

```java
K getKey()//获取Entry对象中的键
V getValue()//获取Entry对象中的值
Set<Map.Entry<K,V>> entrySet()//用于返回Map集合中所有的键值对(Entry)对象，以Set集合形式返回。
```

#### Map 集合遍历键值对

步骤：1.  使用 entrySet() 获取Map集合中所有的键值对(Entry)对象，以Set集合形式返回。2.  遍历包含键值对(Entry)对象的Set集合，得到每一个键值对(Entry)对象。3.  通过键值对(Entry)对象，获取Entry对象中的键与值。

```java
//示例
public static void main(String[] args) {
	Map<String, String> map = new HashMap<String,String>();
	map.put("邓超", "孙俪");
	map.put("李晨", "范冰冰");
	map.put("刘德华", "柳岩");
    Set<Map.Entry<String, String>> set = map.entrySet();
	Iterator<Map.Entry<String, String>> iterator = set.iterator();
	while(iterator.hasNext()){
		Map.Entry<String, String> entry = iterator.next();
		String key = entry.getKey();
		String value = entry.getValue();
		System.out.println(key + " = " + value);
	}
    //增强 for 遍历
    for(Map.Entry<Integer, String> entry : map.entrySet()){
  		System.out.println(entry.getKey()+"..."+entry.getValue());
  	}
}
```



### 集合嵌套

集合嵌套并不是一个新的知识点，仅仅是集合内容又是集合，如Collection集合嵌套、Collection集合与Map集合相互嵌套、Map集合嵌套。

* ArrayList嵌套 ArrayList

  ArrayList< ArrayList<String> >

  Collection< ArrayList<Integer> >

* Map嵌套 ArrayList

  HashMap<String, ArrayList<Person>>

  ArrayList< HashMap<String, String>>

* Map集合嵌套

  HashMap<String, HashMap<String,String>>

  HashMap<String, HashMap<Person,String>>



### Collections 集合工具类

```java
public static <T> void sort(List<T> list) // 集合元素排序
//排序前元素list集合元素 [33,11,77,55]
Collections.sort( list );
//排序后元素list集合元素 [11,33,55,77]

public static void shuffle(List<?> list) //  集合元素存储位置打乱
//list集合元素 [11,33,55,77]
Collections.shuffle( list );
//使用shuffle方法后，集合中的元素为[77,33,11,55]，每次执行该方法，集合中存储的元素位置都会随机打乱

```



### jdk 1.5 新特性

#### 静态导入

```java
//import static XXX.YYY;   导入后YYY可直接使用
//示例：
import static java.util.Map.Entry
//未导入
Set<Map.Entry<Student, String>> entrySet = map.entrySet();
//导入
Set<Entry<Student, String>> entrySet = map.entrySet();
```



#### 可变参数

如果我们定义一个方法需要接受多个参数，并且多个参数类型一致，我们可以对其简化成：修饰符 返回值类型 方法名(参数类型**...** 形参名){  }

这个书写完全等价于：修饰符 返回值类型 方法名(参数类型[] 形参名){  }

只是后面这种定义，在调用时必须传递数组，而前者可以直接传递数据即可。

同样是代表数组，但是在调用这个带有可变参数的方法时，不用创建数组(这就是简单之处)，直接将数组中的元素作为实际参数进行传递，其实编译成的class文件，将这些元素先封装到一个数组中，在进行传递。这些动作都在编译.class文件时，自动完成了。

```java
//示例
public static void main(String[] args) {
	int[] arr = {21,89,32};
	int sum = add(arr);
	System.out.println(sum);
	sum = add(21,89,32);//可变参数调用形式
	System.out.println(sum);		
}
//原始写法
public static int add(int[] arr) {
	int sum = 0;
	for (int i = 0; i < arr.length; i++) {
		sum += arr[i];
	}
	return sum;
}
//可变参数写法
public static int add(int...arr){
	int sum = 0;
	for (int i = 0; i < arr.length; i++) {
		sum += arr[i];
	}
	return sum;
}
```

注意：参数列表只能存在一个可变参数。