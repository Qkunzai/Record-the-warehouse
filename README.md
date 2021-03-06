# Note
本人在初学JAVA语言的各方面的理解与问题
# 初学面向对象
- 类与对象的定义
  - 
 - 相同的东西放在一起称之为一类东西
 - 把一组或多组事物相同的特性的集合的描述称之为类。
 - 类中有很多成员
    类是约束对象有哪些东西组成
    面向过程注重于功能与特性
 - 类是将一组相同的东西抽象出来就是类
 - 类与对象的关系
   - 
 - 类————>对象   称为具象化的过程
 - 对象————>类   称之为抽象化的过程
 - 具象化的过程也叫实例化的过程
 - 代码:
```
 public class main｛
public static void main（String[] args）{
//产生对象 Student 类的对象
Student student1 = new Student();
Student 属于引用类，与引用类的使用方法相同
//赋值
Student1.name = "xu"；
//想两个或多个，只能通过new 创建
Student Student2 = new Student()；
Student student1 = new Stydent();//直接引用构造器
}
｝
```
  - 什么是构造器
   -
  - //构造器在实例化的时候自己调用的，构造器名字必须和类名一致
  - //给当前属性赋初值
  - //构造器没有返回值
  - //构造器实例化时直接初始化字段
```
public Student()｛
System.out.println("构造器");
｝
```
## 面向对象的三大特性
  - 封装
   - 
  - 什么是封装
    - 1.把对象的状态和行为看成一个统一的整体，将二者存放在一个独立的模块中(类)；
    - 2."信息隐藏", 把不需要让外界知道的信息隐藏起来,尽可能隐藏对功能实现细节,字段;
  - 封装的修饰符
    - public private 默认(default) protected
  - 将属性私有化后其他类如何访问此类的属性
    - 创建getchar()方法用来返回属性的值
    - 创建setchar()方法来修改属性的值
  - 继承
    -
  - 什么是继承
    - 继承就是 is a 的关系
    - 将两个类相同的部分抽离出来创建成一个新的类就称之为父类
    - 继承的类称为子类
  - 子类可以使用父类的哪些东西
    - 子类可以使用父类以默认修饰符 public protected修饰符修饰的属性与方法
  - 继承的特性
    - java中继承只有单继承，但可以多层继承如下:

```
public class Father{
    public int nub=0;
}
class Son extends Father{
    public String name = "Boo";
}
public class Student extends Son{
    public static void main(String[] a){
        System.out.println("num="+num+"name="+name);
    }
}
```
- 方法的覆写
   - 子类覆写父类的方法
   - 相当于拓展了父类的成员
- super关键字与this关键字
    - super关键字：
      - 1.表示父类对象的默认引用
      - 2.如果子类要调用父类被覆盖的实例方法，可super 作为调用者调用父类被覆盖的实例方法。
      - 3.使用super调用父类方法
      - 4.使用super调用父类的构造方法
    - this关键字
      - 1.调用本类的方法或字段
      - 2.可以调用本类构造方法，且有一个构造方法要作为出口
      - 3.调用自身构造方法时放在构造方法首行
      - 4.表示当前对象
- 子类对于父类构造器的调用
    - 调用构造方法
    - 本类中调用另一个重载构造方法用this(参数列表)
    - 子类构造方法调用父类构造方法用super(参数列表)
    - 子类调用父类的构造方法时：
    - super必须放在第一句
    - Java在执行子类的构造方法前会先调用父类无参的构造方法，其目的是为了对继承自父类的成员做初始化操作。
    - 子类在创建对象的时候，默认调用父类的无参构造方法，要是子类构造方法中显示指定调用父类其他构造方法，就调用指定的父类构造方法，取消调用父类无参构造方法。
- 多态
  - 
- 什么是多态
  - 多态有两种
    - 运行时多态
      - 方法的覆写
    - 编译时多态
      - 方法的重载
    - 多态就是对象的多种形态如：
```
public class Father{
    int a=0=;
}
class Son extends Father{
    int b =0;
}
public class Student{
  public static void main(String[] a){
  //如可以使用父类来实例化子类，这称为编译时的多态
    Father fa = new Son();
  }
}
```
- 多态的作用
    - 把不同的子类对象都当作父类来看，可以屏蔽不同子类对象之间的差异，写出通用的代码，做出通用的编程，以适应需求的不断变化。
    - 继承是多态产生的前提条件;
- 引用类型转换
    - 向上转型（子类→父类）：(自动完成)
	    父类名称 父类对象 = 子类实例 ;	
    - 向下转型（父类→子类）：(强制完成)
	    子类名称 子类对象 = （子类名称）父类实例 ;
- 多态时方法的调用
  - 当一个引用类型的变量若声明为父类的类型，但实际上引用的是子类的对象(多态情况)：
此时该变量不能再访问子类中自己特有的字段和方法；
若子类覆写了父类的方法，那么此时通过变量访问到的方法，实际上是子类的方法




