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
