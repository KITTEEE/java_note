

## Java 面向对象

#### 类和对象的区别

类是对某一类事物的具体描述，而对象用于表示现实中该类事物的个体。例如一个玩具模型可以做成不同的玩具，其中，玩具模型就可以看作类，而玩具就可以看作对象。



#### 局部变量和成员变量的区别

**区别一：定义位置不同**

局部变量一般定义在方法中或者{}语句里，成员变量一般定义在类中。

**区别二：在内存中的位置不同**

局部变量存储在栈内存的方法中，成员变量存储在堆内存的对象中。

**区别三：声明周期不同**

局部变量随着方法运行出现在栈中，随着方法弹栈而消失。

成员变量随着对象的出现而出现在堆中，随着对象的消失而从堆中消失。

**区别四：初始化不同**

局部变量初始化后没有默认值，须手动赋值后才能使用。成员变量有默认的初始化值，因为在堆内存中。



### 封装

#### 封装的概念

封装是 java 面向对象中的一个重要概念，像机箱里有很多像 CPU 或 主板这样重要的组件，将这些重要组件封装起来，仅仅向外暴露其插口。封装的意思和机箱同理：即只向外提供功能的访问方式，隐藏自己内部的实现细节。使用封装可以提高代码的复用性和安全性。



#### 私有 private

一般我们在创建一个类的对象的时候，对象的属性是都可以直接访问的。private 就是可以让对象的某个属性不能被直接访问的修饰符。

用 private 修饰的变量如果要进行访问，可以用封装的思想，只向外提供访问方式。一般对私有的变量 xxx 的访问方式可以提供对应的 setXxx(赋值)方法 或者 getXxx(取值)方法。



### 继承

**继承描述的是事物之间的所属关系。**例如公司有员工，而员工又可以分为研发部员工或者维护部员工，研发部员工里又可以包含各种不同的工程师，这样在程序中可以描述为研发部员工和维护部员工继承自员工，各种不同的工程师继承自研发部员工或者维护部员工。

继承时需要使用 extends 关键字。一般把继承的类成为子类，被继承的类称为父类，继承之后，子类能拥有父类所有可继承的属性和方法。



#### 继承的注意事项

Java 中只支持单继承，不允许多继承。

多个类可以继承同一个父类。

Java 中允许多层继承，即 B 可继承 A ，C 可继承 B。



#### 继承中，子父类成员变量的特点

* 父类中的成员变量是非私有的，子类可以直接访问，若父类中的成员变量是私有的，则子类不能直接访问。

* 当父类和子类出现了同名的成员变量时，若子类要访问父类的同名成员变量，需使用 super 关键字来完成。表示当前对象引用了父类对象空间。

  ```java
  class Fu { int num = 5; }
  class Zi { 
      int num = 6;
      void show(){
          System.out.println("Fu num ="  + super.num);//访问父类非私有同名成员变量
          System.out.println("Zi num =" + this.num);
      }
  }
  ```



#### 继承中，子父类成员方法的特点(重写等)

**当对象调用方法时，会先在子类中查找有无相应的方法，若存在则会执行子类中的方法，若不存在则会执行父类中相应的方法。**

**方法重写**

**当子类中出现与父类一摸一样的方法时(方法名，参数都相同)，会出现方法的重写(overrride)操作。**子类有自己特有的内容时可以采用重写。

```java
//比如手机来电显示功能，原来只能显示 电话号码，但后期需要在来电显示功能中增加头像和姓名，这时可以重新定义一个描述手机的类并继承原有的类，并重写来电显示功能方法。
class Phone {
    public void showNum() {
        syso("显示号码")；
    }
}
class NewPhone extends Phone {
    public void showNum() {
        super.showNum();//调用父类方法
        syso("显示头像")；
        syso("显示姓名")；
    }
}
```

**方法重写注意事项**

* 子类方法覆盖父类方法，要保证权限大于或等于父类权限

  ```java
  class Fu() { 
      void show(){}
  	public void method() {}
  }
  class Zi extends Fu() {
      public void show() {} //可编译运行
      void method() {} //权限小于父类，编译出错
  }
  ```

* 重写时，方法的返回值类型，方法名，参数列表都要一样。



### 抽象类

有时候，某个父类只知道子类应包含怎样的方法，而不清楚子类会如何实现这些方法。就像一个图形的类，有一个求周长的方法，而不同图形求周长的算法不一样。这时我们便可以考虑把图形类当作一个抽象类。

分析事物时发现了共性的内容时，就可以进行向上抽取，只抽取方法声明而不抽取方法主题，则该被抽取出来的方法便是一个抽象方法。**因此抽象方法只有声明，没有方法体。**

```java
//以研发部员工的共同行为"工作"为例
abstract class Developer {
    public abstract void work();//抽象方法，用 abstract 修饰
}
class JavaEE extends Developer {
    public void work() {...//进行方法主体编写}
}
class Android extends Developer {
	public void work() {...//进行方法主体编写}       
}
```



#### 抽象类的特点

* 抽象类和抽象方法都需要被 abstract 修饰
* 抽象类不可以创建对象，因为调用抽象方法没有意义
* **继承了抽象类的子类，只有重写了所有的抽象方法后，这个子类才可以创建对象，否则这个子类还是一个抽象类。**
* 抽象类一定是一个父类。
* 抽象类中可以不定义抽象方法。（这样做的意义是不会让其他人直接创建该类的对象，）
* 抽象类不可以和 private(私有方法子类继承不到，也就无法重写)、final、static 关键字共存.



### 接口

本来写好了的，结果git reset 了，本地仓库直接没了，有时间再写一遍



### 多态

略



### 构造方法



一般在创建类时，类中的属性都是 private ，外界无法直接访问，只能在创建对象后，通过相应的 set 和 get 方法。**构造方法通常用于在创建对象时就要明确属性值的情况。构造方法就是对象在创建时执行的方法。**



#### 默认的构造方法

在创建指定类的对象时，编译器在编译 java 文件时会自动给 class 文件添加默认的构造方法，如果我们在类的描述中显示指定了构造方法，则编译器不会给 class 文件添加默认的构造方法。



#### 构造方法的细节

* 一个类可以有多个构造方法，它们以重载的形式存在。

* 构造方法可以被 private 修饰，其作用是让其他程序无法创建该类的对象



### this关键字

**成员变量和局部变量同名问题**

在方法中出现了局部变量和成员变量同名的时候，可以在成员变量名前面加上 this. 来区别成员变量和局部变量

**this 代表的是对象，哪个对象调用了 this 所在的方法，this 代表的就是哪个对象。**例如 p.setAge(30) 语句中，setAge(int age) 方法中的 this 代表的就是 对象 p 。



### final关键字

Java 的继承提高了代码的复用性，子类在继承父类后可以对父类中的变量或方法进行重写。如果不想让子类能够重写父类中的某个变量或方法，就可以使用 final 关键字。final 的意思为最终的、不可变的，它可以用来修饰类、类的成员、以及局部变量。



#### final使用特点

* 用 final 修饰过的类不能被继承，但可以继承其他类。

```java
class Yy {}
final class Fu extends Yy {}
class Zi extends Fu {} //不能被继承
```

* 父类中用 final 修饰的方法，子类继承后不能重写；父类中没有被 final 修饰的方法，子类重写后可添加 final 修饰

```java
class Fu() {
    public final void method1() {}
    public void method2() {}
}
class Zi extends Fu() {
    public final void method2(){}//重写 method2 方法并添加 final 修饰
}
```

* final 修饰的变量为常量，只能赋值一次；final 修饰的成员变量须在创建对象前赋值，否则报错

```java
final int i = 1;
i = 2;//报错

class Demo () {
    final int m = 100;
    final int n;//没有赋值(没构造方法)会报错
    public Demo() {
        n = 2016;//可在创建对象所调用的构造方法中为 final 成员变量赋值
    }
}
```



### static关键字

#### static的特点

* **被 static 修饰的成员变量不属于类的某个对象，而是属于类。**也就是说假如某个对象修改了类中的 static 成员变量，其他对象中的 static 成员变量也会跟着改变。
* 被 static 修饰的成员变量可以并且建议直接通过类名访问。  

```java
class Demo {
    public static int num = 100;
    public static void method() {
        Syso("静态方法");
    }
}
class Test {
    public static void main(String[] args) {
        Demo d1 = new Demo();
        Demo d2 = new Demo();
        d1.num = 200;
        Syso(d1.num);
        Syso(d2.num);//200
        Syso(Demo.num);//200
    	Demo.method();//静态方法
    }
}
```



#### static 注意事项

* 静态内容是优先与对象的存在，静态修饰的内容存在于静态区，**不能使用 this / super 访问静态变量**。

* 静态成员只能访问静态成员(如：静态方法中只能访问静态成员变量或静态成员方法)。
* main 方法为静态方法仅仅为程序执行入口，它不属于任何一个对象，可以定义在任意类中。

```java
class Demo {
    public int num1 = 10;
    public static int num2 = 20;
    public static void method() {
        Syso(num1);//无法访问
        Syso(num2);//20
    }
}
```



#### 静态常量

* 定义静态常量一般用 public static final 来定义，此时变量名全部用大写，多个单词用下划线连接。

* 接口中的每个成员变量都默认使用 public static final 修饰，所有接口中的成员变量都已经是常量，由于接口没有构造方法，因此需要显示赋值。接口的静态常量可以直接用接口名访问。

```java
public static final String SCHOOL_NAME = "SCSU"//定义静态常量
interface inter {
	public static final int count = 1;    
}
inter.count;//可以直接用接口名访问
```



### 匿名对象

匿名对象指的是在创建对象时只有创建语句，但并没有把对象地址赋值给某个变量。

```java
Person p = new Person();//创建普通对象
new Person();//创建匿名对象
```



#### 匿名对象特点

* 匿名对象可直接调用方法
* 匿名对象在没有指定其引用对象时只能使用一次
* 匿名对象可以作为方法接收的参数和方法的返回值

```java
new Person().eat();//对象直接调用方法
class Demo {
    public static Person getPerson(){
    	return new Person();
    }
    public static void method(Person p) {
        
    }
}
class Test {
    public static void main(String args[]) {
        Person p = Demo.getPerson();//接收方法的返回值
     	Demo.method(new Person());//作为方法接收的参数   
    }
}
```



### 内部类

略



### 修饰符访问权限

|                        | public | protected | default | private |
| :--------------------: | ------ | --------- | ------- | ------- |
|        同一类中        | T      | T         | T       | T       |
| 同一包中(子类与无关类) | T      | T         | T       |         |
|      不同包的子类      | T      | T         |         |         |

