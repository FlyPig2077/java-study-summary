## 修饰符

### 一、修饰符介绍

修饰符用来定义类、方法或者变量，通常放在语句的最前端，主要分为两类：

* 访问修饰符
* 非访问修饰符

例子：

```java
public class ClassName {
   // ...
}
private boolean myFlag;
static final double weeks = 9.5;
protected static final int BOXWIDTH = 42;
public static void main(String[] arguments) {
   // 方法体
}
```

### 二、访问控制修饰符

Java中，可以使用访问控制符来保护对**类、变量、方法和构造方法**的访问。Java 支持 4 种不同的访问权限。

- **default** (即默认，什么也不写）: 在同一包内可见，不使用任何修饰符。使用对象：类、接口、变量、方法。
- **private** : 在同一类内可见。使用对象：变量、方法。 **注意：不能修饰类（外部类）**
- **public** : 对所有类可见。使用对象：类、接口、变量、方法
- **protected** : 对同一包内的类和所有子类可见。使用对象：变量、方法。 **注意：不能修饰类（外部类）**。

| 修饰符    | 类内部 | 同个包（package） | 子类           | 其他范围 |
| --------- | ------ | ----------------- | -------------- | -------- |
| public    | Y      | Y                 | Y              | Y        |
| protected | Y      | Y                 | Y              | N        |
| 无修饰符  | Y      | Y                 | Y或者N(见说明) | N        |
| private   | Y      | N                 | N              | N        |

#### 1、protected 

对同一包内的类和所有子类可见。使用对象：变量、方法。 **注意：不能修饰类（外部类）**。

子类能访问 protected 修饰符声明的方法和变量，这样就能保护不相关的类使用这些方法和变量。

使用场景：如果我们只想让**该方法对其所在类的子类可见**，则将该方法声明为 protected。

```java
class AudioPlayer {
   protected boolean openSpeaker(Speaker sp) {
      // 实现细节
   }
}
 
class StreamingAudioPlayer extends AudioPlayer {
   protected boolean openSpeaker(Speaker sp) {
      // 实现细节
   }
}
```

1. protected 访问控制符能被用于方法和成员变量。

2. 声明为protected的方法和成员变量能被同一个包里的所有类所访问，就像默认修饰符package一样。

3. 能被该类的子类所访问，子类可以和父类不在一个包中。

　　这样，当你想让一个类中的某个方法或成员变量在包中都可见，而且其子类也能访问（子类有可能和父类不在同一个包中）但又不想让所有类都可以访问该类时，就可以用protected修饰符。

#### 2、private

* 被声明为 **private** 的方法、变量和构造方法只能被所属类访问，并且类和接口不能声明为 **private**。
* 声明为私有访问类型的变量只能通过类中公共的 getter 方法被外部类访问。
* Private 访问修饰符的使用主要用来隐藏类的实现细节和保护类的数据。

### 三、非访问修饰符

* static 修饰符，用来修饰类方法和类变量。

* final 修饰符，用来修饰类、方法和变量，final 修饰的类不能够被继承，修饰的方法不能被继承类重新定义，修饰的变量为常量，是不可修改的。

* abstract 修饰符，用来创建抽象类和抽象方法。

* synchronized 和 volatile 修饰符，主要用于线程的编程。

#### 1、static 修饰符

- **静态变量：**

  static 关键字用来声明独立于对象的静态变量，无论一个类实例化多少对象，它的静态变量只有一份拷贝。 静态变量也被称为类变量。**局部变量不能被声明为 static 变量**。

- **静态方法：**

  static 关键字用来声明独立于对象的静态方法。静态方法不能使用类的非静态变量。静态方法从参数列表得到数据，然后计算这些数据。（**调用静态方法不用创建对象**）

#### 2、final修饰符

**final变量：**

final 表示"最后的、最终的"含义，变量一旦赋值后，**不能被重新赋值**。被 final 修饰的实例变量必须显式指定初始值。

final 修饰符通常和 static 修饰符一起使用来创建类常量。

**final方法：**

父类中的final方法可以被子类继承，但是不能被子类重写

声明final方法的主要目的是**防止该方法的内容被修改**

**final 类**

**final 类不能被继承**，没有类能够继承 final 类的任何特性。

#### 3、abstract修饰符

**抽象类：**

**抽象类不能用来实例化对象**，声明抽象类的唯一目的是为了将来对该类进行扩充。

一个类不能同时被 abstract 和 final 修饰。如果一个类包含抽象方法，那么该类一定要声明为抽象类，否则将出现编译错误。

抽象类可以包含抽象方法和非抽象方法。

**抽象方法：**

抽象方法是一种没有任何实现的方法，该方法的的具体实现由子类提供。

抽象方法不能被声明成 final 和 static。

任何继承抽象类的子类必须实现父类的所有抽象方法，除非该子类也是抽象类。

如果一个类包含若干个抽象方法，那么该类必须声明为抽象类。抽象类可以不包含抽象方法。

#### 4、synchronized 修饰符

synchronized 关键字声明的方法同一时间只能被一个线程访问。synchronized 修饰符可以应用于四个访问修饰符。

#### 5、transient 修饰符

序列化的对象包含被 transient 修饰的实例变量时，java 虚拟机(JVM)跳过该特定的变量。

该修饰符包含在定义变量的语句中，用来预处理类和变量的数据类型。

```java
public transient int limit = 55;   // 不会持久化
public int b; // 持久化
```

#### 6、volatile修饰符

volatile修饰的成员变量在每次被线程访问时，都强制从共享内存中重新读取该成员变量的值。而且，当成员变量发生变化时，会强制线程将变化值回写到共享内存。**这样在任何时刻，两个不同的线程总是看到某个成员变量的同一个值。**

```java
public class MyRunnable implements Runnable
{
    private volatile boolean active;
    public void run()
    {
        active = true;
        while (active) // 第一行
        {
            // 代码
        }
    }
    public void stop()
    {
        active = false; // 第二行
    }
}
```

通常情况下，在一个线程调用 run() 方法（在 Runnable 开启的线程），在另一个线程调用 stop() 方法。 如果 ***第一行\*** 中缓冲区的 active 值被使用，那么在 ***第二行\*** 的 active 值为 false 时循环不会停止。

但是以上代码中我们使用了 volatile 修饰 active，所以该循环会停止。