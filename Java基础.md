# 数据类型

| 基础数据类型 | 所占字节数                            |
| ------------ | ------------------------------------- |
| byte         | 1                                     |
| short        | 2                                     |
| int          | 4                                     |
| long         | 8                                     |
| float        | 4                                     |
| double       | 8                                     |
| char         | 2 因为要同时表示ASCII和Unicode        |
| boolean      | 理论上1bit，通常JVM会表示成四字节整数 |

| 引用类型 | 描述                                                         |
| -------- | ------------------------------------------------------------ |
| String   | 不可变，指向null表示不存在                                   |
| 数组     | int[] numbers = new int[5];                                  |
|          | int[] numbers = new int[] { 68, 79, 91, 85, 62 };            |
|          | int[] numbers = {68,79,91,85,62};                            |
|          | 对于字符串数组中的每一个元素都指向一个String对象![image-20220119143558960](C:\Users\wifePie\AppData\Roaming\Typora\typora-user-images\image-20220119143558960.png) |
|          |                                                              |

# 关键字

| 关键字 | 用处     |
| ------ | -------- |
| var    | 类比auto |
| final  | 变常量   |

# 输出

# 输入

```java
Scanner scanner = new Scanner(System.in) ;
String name = scanner.nextLine() ;
int age = scanner.nextInt() ;
```

# 面向对象

## 构造方法

构造的顺序

* 初始化字段然后
* 执行构造方法的代码进行初始化

## 继承

* 严禁定义和父类同名字段

* 子类执行构造函数的时候，如果没有显示调用 super() 那么，系统会自动调用。

* 所以如果要在构造子类的同时构造父类，那么就需要在子类构造中显式调用super() 以达到父类构造的效果

## 向上/下转型

子类可以向上转型成父类（因为子类功能更多，父类有的他都有）

父类不一定能转型成子类

转型之前可以先用 **instanceof** 判断一下

![image-20220119155146266](https://s2.loli.net/2022/01/19/q8PRQD5yn94xWMj.png)

## 多态

### 覆写 override

在继承关系中，子类定义了一个和父类方法签名完全相同的方法。

![image-20220119160703024](https://s2.loli.net/2022/01/19/K62EueaZI9J5RyT.png)

### 重载 overload

功能类似的方法使用同一个名字，但是方法的签名不同。主要目的是为了更易记忆和调用。

### 多态 Polymorphic

针对某个类型的方法调用，其真正执行的方法取决于运行时期实际类型的方法。

```java
public class Main {
    public static void main(String[] args) {
        Person p = new Student();
        p.run(); // 应该打印Person.run还是Student.run?
    }
}

class Person {
    public void run() {
        System.out.println("Person.run");
    }
}

class Student extends Person {
    @Override
    public void run() {
        System.out.println("Student.run");
    }
}
```

```java
//实际输出：
Student.run
```

## final

* 用final修饰的方法不能被override
* 用final修饰的类不能被继承

## 抽象类

使用 abstract 修饰的类就是抽象类，抽象类不能被实例化。

使用 abstract 修饰的方法是抽象方法，抽象方法没有具体执行代码。

抽象类可以强迫它的子类实现其定义的抽象方法。

## 接口 interface

如果一个抽象类全是抽象方法而没有字段，就可以把该抽象类改写成接口。

一个类不可以继承多个类，但是可以实现多个接口。

### default

在接口中可以定义 default 方法

```java
public class Main {
    public static void main(String[] args) {
        Person p = new Student("Xiao Ming");
        p.run();
    }
}

interface Person {
    String getName();
    default void run() {
        System.out.println(getName() + " run");
    }
}

class Student implements Person {
    private String name;

    public Student(String name) {
        this.name = name;
    }

    public String getName() {
        return this.name;
    }
}
```

目的是，当我们需要给接口新增一个方式时，会涉及到修改全部子类。如果新增的是$default$方法，那么子类就不必全部修改，只需要在需要覆写的地方覆写新增方法。

## 静态字段和静态方法

静态实例可以理解成被引用了

静态方法则是不需要通过实例调用，可以通过类名.方法的形式调用。在静态方法的内部只能访问静态字段，无法访问$this$变量

### 关于接口

接口不能定义实例字段，但是可以有静态字段，类型都默认为 $public$ $static$ $final$

## 包 Package

