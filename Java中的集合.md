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