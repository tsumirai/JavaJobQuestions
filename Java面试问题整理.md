# 继承、抽象类与接口区别、访问控制、多态相关
1. 接口和抽象类的区别

* 语法层次：

抽象类中可以拥有任意范围的成员数据，可以定义非抽象方法。而接口中只能拥有静态的不能修改的成员数据，同时所有的方法必须是抽象的。所以说接口是抽象类的一种特例。
* 跨域不同

抽象类是对类的整体进行抽象，包括类的属性和行为。接口是对类的局部（行为）进行抽象。
抽象类是is-a，跨域的是具有相似特点的类。接口是like-a，可以跨域不同的类。
例如猫、狗可以抽象成一个动物类的抽象类，具备叫的方法。鸟、飞机可以实现Fly接口，具备飞的行为。
* 设计层次

抽象类是自下而上的一种设计思想，而接口是自顶而下的一种设计思想。
抽象类中我们要知道子类才能抽象出父类。而接口不同，它只需要定义一个规则即可。

2. 是否可以实现多个接口，是否可以继承多个抽象类。

Java可以实现多个接口，但是对于类是单继承体系结构。

3. 静态内部类和内部类的不同

静态内部类没有了指向外部类的引用，可以直接被实例化而不需要依附于外部类的实例化。
非静态内部类保留了指向外部类的引用，必须依附于外部类的实例化才能够实例化内部类。
静态嵌套类内部中：内部类不能访问外部类的非静态成员。外部类不能直接访问静态类中的属性，需要通过内部类去访问。
非静态内部类中：内部类可以直接访问外部类的属性成员。外部类不能直接方位静态类中的属性，需要通过内部类去访问。
延伸：使用内部类最吸引人的原因是：每个内部类都能独立地继承一个类，所以无论外围类是否已经继承某个类，对内部类都没有影响。
内部类：成员内部类（直接在外部类中）、局部内部类（内部类在方法或者作用域中）、嵌套内部类（static修饰的内部类）、匿名内部类。

4. 局部内部类和匿名内部类访问局部变量时，为何需要加final关键字？

局部变量的生命周期与局部内部类的对象的生命周期的不一致性。例如内部类innerClass在方法f()中，而方法f()中定义局部变量i且被内部类使用。当方法f()运行结束后，局部变量i就已经死亡不存在了，但局部内部类对象可能还存在（直到没有人再引用该对象才会消亡）,这时出现一种情况就是局部内部类要访问一个已经不存在的局部变量。而当变量被final修饰时，通过final将局部变量“复制”一份，复制品直接作为局部变量中的数据成员。

5. Overload和Override的区别。Overloaded的方法是否可以改变返回值的类型？

overload重载和override重写是Java多态性的不同表现。
overload是一个类多态性的表现，override是父类和子类多态性的表现。
override：子类中定义与父类相同的名称及签名。

overload：方法相同，方法签名不同。
注意：不能通过访问权限、返回类型、抛出的异常进行重载。
static修饰的方法不能够被重写。

6. abstract的method是否可同时是static，是否可同时是native，是否可同时是synchronized

都不可以。因为abstract申明的方法是要求子类去实现的，abstract只是告诉你有这样一个接口，你要去实现，至于你的具体实现可以使native和synchronized，也可以不是。抽象方法是不关心这些事的，所以写这两个是没有意义的。然后，static方法是不会被重写的，而abstract方法正是要子类去重写它，所以也是没有意义的。所以，总的来说，就是java语法不允许你这样做，事实上，也没有这样做的意义。
abstract需要重写，static为类方法，没有重写一说
abstract为没有实现的方法，native为本机实现的方法，自相矛盾。
abstract方法没有实现，也不可能实际调用抽象方法，没有必要synchronized修饰，当然子类可以根据需要同步该方法。

7. 接口是否可以继承接口？抽象类是否可以实现接口？抽象类是否可以继承实体类？

接口可以继承接口。
抽象类可以实现接口。
抽象类可以继承实体类，但前提是实体类必须有明确的构造函数。

8. 构造器Constructor是否可被override？

构造器Constructor不能被继承，因此不能重写（Override），但可以被重载（Overload）。

9. 启动一个线程是用run()还是start()？

启动一个线程是调用start()方法，使线程所代表的的虚拟处理机处于可运行状态，这意味着它可以由JVM调度并执行。这并不意味着线程就会立即运行。run()方法可以产生必须退出的标志来停止一个线程。

10. 作用域public，protected，private，以及不写时的区别？

不写时默认是包权限。

作用域 | 当前类 | 同一package | 子孙类 | 其他package
:-: | :-: | :-: | :-: |:-:
public | √ | √ | √ | √ |
protected | √ | √ | √ | × |
friendly | √ | √ | × | × |
private | √ | × | × | × |

这里需要说明的是，在同一个package，public、protected、friendly使用范围一致。而在其他package中，只有子孙类中的protected才能被访问。

# collections相关的数据结构及API
1. 列举几个Java Collection类库中的常用类

Collection是java.util中的一个接口，继承自Iterable。
子接口：List、Set、Queue...
实现类：ArrayList、LinkedList、HashSet、TreeSet、Vector、Stack
其他相关类：Iterator、TreeMap、HashTable、HashMap
Collection接口是最基本的集合接口，它不提供直接的实现，Java SDK提供的类都是继承自Collection的“子接口”。如List和Set。Collection所代表的是一种规则，它所包含的元素都必须遵循一条或者多条规则。如有些允许重复而有些则不能重复，有些必须要按照顺序插入而有些则是散列，有些支持排序但有些则不支持。

2. List、Set、Map是否都继承自Collection接口？

List、Set继承自Collection接口，而Map不是。

* List所代表的是有序的Collection。实现List接口的集合主要有：ArrayList、LinkedList、Vector、Stack。
* Set是一种不包括重复元素的Collection。实现了Set接口的集合有：EnumSet、HashSet、TreeSet。
* Map与List、Set接口不同，它是由一系列键值对组成的集合，提供了key到value的映射。同时它也没有继承Collection。实现Map的有：HashMap、TreeMap、HashTable、Properties、EnumMap。

3. HashMap和HashTable的区别。

* 历史原因：HashTable是基于陈旧的Dictionary类的，HashMap是Java1.2引进的Map接口的一个实现。
* 同步性：HashTable是线程安全的，也就是说是同步的，而HashMap是线程不安全的，不是同步的。
* 值：只有HashMap可以将空值作为一个表的条目的key或value。

* HashTable的方法是同步的，在方法的前面都有Synchronized来同步；HashMap未经同步，所以在多线程场合要手动同步。
* HashTable不允许null值（key和value都不可以），HashMap允许null值（key和value都可以）。
* HashTable有一个contains（Object value）功能和contaiValue（Object value）功能一样。
* HashTable使用Enumeration进行遍历，HashMap使用Iterator进行遍历。
* HashTable中hash数组默认大小是11，增加的方式是old*2+1。HashMap中hash数组的默认大小是16，而且一定是2的指数。
* hash值的使用不同，HashTable直接使用对象的hashCode，代码是这样的：

```java
int hash = key.hashCode();
int index = (hash & 0X7FFFFFFF) % tab.length;
```
而HashMap重新计算hash值，而且用与代替求模：

```java
int hash = hash(k);
int i = indexFor(hash, table.length);
static int hash(Object x) {
    h ^= (h >>> 20) ^ (h >>> 12 );
    return h ^ (h >>> 7) ^ (h >>> 4);
}
```

* 延展： 

### HashMap与HashSet的关系
* HashSet底层是采用HashMap实现的
```java
public HashSet() {
    map = new HashMap<E,Object>();
}
```        
* 调用HashSet的add方法时，实际上是向HashMap中增加了一行（key-value对），该行的key就是向HashSet增加的那个对象，该行的value就是一个Object类型的常量。

```java
private static final Object PRESENT = new Object();
public boolean add(E e) {
    return map.put(e, PRESENT) == null;
}

public boolean remove(Object o) {
    return map.remove(o) = PRESENT;
}
```

### HashMap和ConcurrentHashMap的关系
ConcurrentHashMap也是一种线程安全的集合类，它和HashTable也是有区别的，主要区别就是加锁的粒度以及如何加锁。ConcurrentHashMap的加锁粒度要比HashTable更细一点。将数据分成一段一段地存储，然后给每一段数据配一把锁，当一个线程占用锁访问其中一个段数据的时候，其他段的数据也能被其他线程访问。

