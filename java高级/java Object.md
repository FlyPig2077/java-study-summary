## Java Object类

java Object 类是所有类的父类，也就是说Java的所有类都继承了Object，子类可以使用Object的所有方法

Object 类位于 java.lang 包中，编译时会自动导入，我们创建一个类时，如果没有明确继承一个父类，那么它就会自动继承 Object，成为 Object 的子类。

**类的方法：**

* protected Object clone()：创建并返回一个对象的拷贝
* boolean equals(Object obj)：比较两个对象是否相等
* protected void finalize()：当GC（垃圾回收器）确定不存在对该对象的有更多引用时，由对象的垃圾回收器调用此方法
* Class<?> getClass()：获取对象的运行时对象的类
* int hasCode()：获取对象的 hash 值
* void notify()：唤醒在该对象上等待的某个线程
* void notifyAll()：唤醒在该对象上等待的所有线程
* String toString()：返回对象的字符串表示形式
* void wait()：让当前线程进入等待状态，知道其他线程调用此对象的notify()方法或notifyAll()方法
* void wait(long timeout)：让当前线程处于等待(阻塞)状态，直到其他线程调用此对象的 notify() 或 notifyAll() 方法，或者超过参数设置的timeout超时时间
* void wait(long timeout, int nanos)：与 wait(long timeout) 方法类似，多了一个 nanos 参数，这个参数表示额外时间（以纳秒为单位，范围是 0-999999）。 所以超时的时间还需要加上 nanos 纳秒（其主要作用应该在能更精确控制等待时间）

**面试题：**

参考：https://blog.csdn.net/xl_1803/article/details/80445481

https://blog.csdn.net/Rex_WUST/article/details/95739535

https://blog.csdn.net/VIP_WangSai/article/details/77505517

1、为什么重写了equals()也要重写hashCode()

**在重写equals时，需要重写hashCode，不然会出现与预期不符的结果**，以保证他们是相同的比较逻辑

HashMap是底层实现时数组加链表。
    A.当put元素时:
       1.首先根据put元素的key获取hashcode,然后根据hashcode算出数组的下标位置,如果下标位置没有元素，直接放入元素即可。
       2.如果该下标位置有元素（即根据put元素的key算出的hashcode一样即重复了），则需要已有元素和put元素的key对象比较equals方法，如果equals不一样，则说明可以放入进map中。这里由于hashcode一样，所以得出的数组下标位置相同。所以会在该数组位置创建一个链表，后put进入的元素到放链表头，原来的元素向后移动。    
     B.当get元素时:
       根据元素的key获取hashcode，然后根据hashcode获取数组下标位置，如果只有一个元素则直接取出。如果该位置一个链表，则需要调用equals方法遍历链表中的所有元素与当前的元素比较,得到真正想要的对象。
可以看出如果根据hashcdoe算出的数组位置尽量的均匀分布，则可以避免遍历链表的情况，以提高性能。
所以 要求重写hashmap时，也要重写equals方法。以保证他们是相同的比较逻辑

​      主要是为了hashmap或者hashset避免逻辑上冲突吧，比如你创建一个Map然后new一个student对象，赋唯一属性，如姓名身高体重，然后给定学号map.put(stu,23)，当你get(stu)就能得到该学生学号，这时候你又new了一个一模一样的人也是就student，如果不重写hashcode，那么会默认用hash地址算法，得到的不一样的hashcode值，这时候你get这个学生的学号就无法get到了，因为hashcode不同

**equals方法：**

`Object`类中的`equals()`方法定义如下:

```java
public boolean equals(Object obj) {
    return (this == obj);
}
```

- 基本数据类型：比较的是`==`两边值是否相等
- 引用数据类型：比较的是`==`两边内存地址是否相等

所有要实现自己的`equals()`方法都要遵守下面几个规则

- 自反性：对于任何对象x，`x.equals(x)`应该返回`true`
- 对称性：对于任何两个对象x和y，如果`x.equals(y)`返回`true`，那么`y.equals(x)`也应该返回`true`
- 传递性：对于多个对象x,y,z，如果`x.equals(y)`返回`true`,`y.equals(z)`返回`true`，那么`y.equals(z)`也应该返回`true`
- 一致性：对于两个非空对象x,y，在没有修改此对象的前提下，多次调用返回的结果应该相同
- 对于任何非空的对象x，`x.equals(null)`都应该返回`false`

**hashCode方法：**

`Object`中的`hashCode()`方法是一个本地方法，返回一个`int`类型的哈希值。

* `hashCode`：用来计算该对象放入数组中的哪个位置

```java
public native int hashCode();
```

这两个方法经常出现在`HashMap`中