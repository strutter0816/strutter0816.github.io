# 被问到（倒）的面试题以及疑难杂症


<!--more-->

## 重载和重写的区别

- 重写(Overriding)是”外壳不变，核心重写”,即在**子类存在方法与父类的方法的名字相同,**而且**参数的个数与类型一样,返回值也一样**的方法。

- 重载(overloading) 是**在一个类里面，方法名字相同，而参数不同。**返回类型可以相同也可以不同。

## HashMap的put实现流程

1. **计算Key的哈希值：** 首先，HashMap会调用Key的`hashCode()`方法来获取Key的哈希码（hash code）。
2. **计算哈希值的索引位置：** 使用哈希值和HashMap的容量进行计算，确定存储位置。具体计算方法是取哈希值对容量取余数，这个余数就是键值对应的数组索引。
3. **处理冲突：** 如果发现两个不同的Key计算得到相同的索引位置，发生了哈希冲突。HashMap使用链表或红黑树等数据结构来解决冲突。
4. **插入键值对：** 如果在特定位置没有冲突，或者已经通过链表或树解决了冲突，就将键值对插入到相应的位置。
5. **检查是否需要进行扩容：** 如果插入键值对后，HashMap的大小超过了某个阈值，就会触发HashMap的扩容操作，以保持哈希表的负载因子在可接受范围内。

## Mysql的数据结构和索引

1. 最基本的是表，表是由行列组成的，每一行表示一条记录，每一列表示记录中的一个属性。表的数据结构可以简单描述为二维表格、
2. 索引是一种用于加速数据检索的数据结构
   1. **B树索引：** 大多数情况下，MySQL使用B树（或B+树）作为索引的数据结构。B树是一种平衡树结构，它可以快速定位到目标值。B+树相较于B树在内部节点只存储索引字段的值，而数据都存储在叶子节点，这样可以提高范围查询的性能。
   2. **哈希索引：** MySQL也支持哈希索引，但有一些限制。哈希索引适用于等值查询，但不支持范围查询，也无法按顺序存储数据。
   3. **全文索引：** 用于全文搜索的索引类型，例如`FULLTEXT`索引。它允许对文本列进行全文搜索，而不仅仅是简单的等值匹配。
   4. **空间索引：** 用于地理空间数据类型的索引，例如`SPATIAL`索引。

## java的抽象类和接口类的区别

### 抽象类（Abstract Class）：

1. **定义：** 抽象类是用于表示一种抽象概念的类，它不能被实例化，只能被继承。抽象类可以包含抽象方法（没有实现的方法）和具体方法（有实现的方法）。

2. **关键特点：**

   - 抽象类可以包含成员变量和普通方法。
   - 抽象方法用 `abstract` 关键字声明，子类必须实现抽象方法。
   - 抽象类的构造函数在子类中被调用时会执行，但抽象类本身不能被实例化。

3. **继承：** 一个类只能继承一个抽象类。

4. **例子：**

   ```java
   abstract class Animal {
       String name;
       
       abstract void makeSound(); // 抽象方法
       
       void eat() {
           System.out.println("Animal is eating.");
       }
   }
   ```

### 接口（Interface）：

1. **定义：** 接口是一种完全抽象的类，它定义了一组方法的签名，但没有提供方法的具体实现。接口中的所有方法都默认是 `public` 和 `abstract` 的。

2. **关键特点：**

   - 接口中只能包含常量（`static final`）和抽象方法。
   - 接口中的方法默认是 `public` 和 `abstract` 的，可以省略这些关键字。
   - 类实现接口时，必须提供接口中所有方法的具体实现。

3. **实现：** 一个类可以实现多个接口。

4. **例子：**

   ```java
   interface Animal {
       void makeSound(); // 抽象方法
       
       default void eat() {
           System.out.println("Animal is eating.");
       }
   }
   ```

### 区别总结：

1. **多继承：** 类可以继承一个抽象类，但只能实现多个接口。Java中不支持多继承，但通过接口可以实现类似的效果。
2. **构造函数：** 抽象类有构造函数，接口没有。抽象类的构造函数在子类实例化时会被调用，而接口没有构造函数。
3. **成员变量：** 抽象类可以包含成员变量，而接口只能包含常量。
4. **默认实现：** 接口中可以包含默认实现的方法（使用 `default` 关键字），而抽象类中的方法默认需要在子类中实现。

## C++有没有java中继承和实现一说

在C++中，有继承（inheritance）的概念，但和Java一样，C++中的继承并没有像Java那样的"implements"关键字，而是使用"派生类（子类）继承基类（父类）"的方式。

C++中的继承分为两种主要类型：

1. **公有继承（Public Inheritance）：** 使用`public`关键字表示。在公有继承中，派生类（子类）可以访问基类（父类）的公有成员和受保护成员。这种继承关系符合"is-a"关系。

   ```c++
   // 基类
   class Base {
   public:
       int publicMember;
   protected:
       int protectedMember;
   private:
       int privateMember;
   };
   
   // 派生类
   class Derived : public Base {
       // Derived 可以访问 Base 的 publicMember 和 protectedMember
   };
   ```

2. **私有继承（Private Inheritance）：** 使用`private`关键字表示。在私有继承中，基类的公有和保护成员在派生类中都变成了私有成员。这种继承关系通常用于实现"has-a"关系，而不是"is-a"关系。

   ```c++
   class Derived : private Base {
       // Base 的所有成员在 Derived 中都变为私有成员
   };
   ```

在C++中，类可以继承多个类，这被称为多重继承。多重继承可能导致菱形继承问题，为了解决这个问题，C++引入了虚继承（virtual inheritance）。虚继承允许在继承体系中共享基类的实例，以避免派生类中包含多个实例的问题。

## Java怎么加锁

在 Java 中，有几种方式可以加锁，其中最常用的是使用 `synchronized` 关键字和 `ReentrantLock` 类。这两种方式都可以用来保护共享资源，防止多个线程并发访问导致的竞态条件。

### 1. 使用 `synchronized` 关键字：

`synchronized` 关键字可以用来修饰方法或代码块，以实现对共享资源的加锁。下面是两种使用 `synchronized` 的方式：

#### a. 修饰方法：

```java
public class SynchronizedExample {
    private int count = 0;

    public synchronized void increment() {
        count++;
    }

    public synchronized int getCount() {
        return count;
    }
}
```

#### b. 修饰代码块：

```java
public class SynchronizedExample {
    private int count = 0;
    private Object lock = new Object();

    public void increment() {
        synchronized (lock) {
            count++;
        }
    }

    public int getCount() {
        synchronized (lock) {
            return count;
        }
    }
}
```

### 2. 使用 `ReentrantLock` 类：

`ReentrantLock` 是 `java.util.concurrent.locks` 包中提供的一种加锁机制。相比于 `synchronized`，`ReentrantLock` 提供了更多的灵活性和功能，但使用时需要注意及时释放锁，以避免死锁的发生。

```java
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

public class ReentrantLockExample {
    private int count = 0;
    private Lock lock = new ReentrantLock();

    public void increment() {
        lock.lock();
        try {
            count++;
        } finally {
            lock.unlock();
        }
    }

    public int getCount() {
        lock.lock();
        try {
            return count;
        } finally {
            lock.unlock();
        }
    }
}
```

无论是使用 `synchronized` 还是 `ReentrantLock`，都是为了保护共享资源，防止多个线程同时修改导致的并发问题。选择哪种方式取决于具体的需求和场景。在简单情况下，`synchronized` 可能更为方便，而在需要更多控制和功能的情况下，`ReentrantLock` 提供了更多选项。

## Synchronized和ReentrantLock两个的实现原理是什么

`Synchronized` 和 `ReentrantLock` 都是用来进行线程同步的工具，但它们的实现原理有一些差异。

### 1. Synchronized 的实现原理：

- **内部锁（Monitor）：** 在 Java 中，每个对象都有一个与之关联的内部锁，也称为监视器锁（Monitor Lock）或对象锁。当一个线程进入被 `synchronized` 修饰的方法或代码块时，它会尝试获取对象的锁。如果锁已经被其他线程占用，那么线程将被阻塞，直到锁被释放。
- **对象头标记：** 对象头中包含了用于存储锁信息的字段。当线程尝试获得锁时，JVM 会检查对象头中的锁标记。如果锁未被占用，线程获得锁并继续执行。如果锁已被其他线程占用，线程将被放入等待队列，等待锁的释放。
- **可重入性：** `Synchronized` 具有可重入性，同一线程可以多次获取同一个对象的锁，而不会导致死锁。

### 2. ReentrantLock 的实现原理：

- **AQS（AbstractQueuedSynchronizer）：** `ReentrantLock` 是基于 AQS 框架实现的。AQS 是 Java 中用于构建锁和其他同步器的框架。它使用了一个双向队列来管理等待锁的线程。
- **独占锁：** `ReentrantLock` 是一种独占锁（Exclusive Lock），同一时刻只有一个线程可以获得锁。当线程尝试获取锁时，如果锁已经被其他线程占用，它将被放入等待队列，而不是一直忙等。
- **Condition：** `ReentrantLock` 还提供了 `Condition` 对象，可以用于实现更灵活的线程通信。
- **可中断性：** `ReentrantLock` 支持可中断的获取锁操作，线程可以通过 `lockInterruptibly` 方法中断等待锁的过程。

## TCP/IP 三次握手和四次挥手

![img](https://img2018.cnblogs.com/blog/1217276/201905/1217276-20190503210424740-1764008697.jpg)

![img](https://img2018.cnblogs.com/blog/1217276/201905/1217276-20190503231436105-1355677452.png)

