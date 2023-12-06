# 被问到（倒）的面试题以及疑难杂症


<!--more-->

# Java

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

# C++

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

# 计算机网络

## 网络协议

IP协议，TCP协议，UDP协议，HTTP协议

**TCP/IP**协议是传输层协议，主要解决数据如何在网络中传输，**HTTP**是应用层协议，主要解决如何包装数据

### IP协议

IP协议的作用在于把各种数据包准备无误的传递给对方，其中两个重要的条件是IP地址和MAC地址

### TCP协议

TCP（传输控制协议）是面向连接的传输层协议。两部分组成 首部和数据  不同主机的应用层之间经常需要可靠的、像管道一样的连接，但是IP层不提供这样的流机制，而是提供不可靠的包交换。TCP协议采用字节流传输数据。

### TCP 三次握手建立连接和四次挥手关闭



![img](https://raw.githubusercontent.com/strutter0816/githubPngImags/main/img/202312062247556.jpeg)

<img src="https://raw.githubusercontent.com/strutter0816/githubPngImags/main/img/202312062249215.png" alt="img" style="zoom:80%;" />

### 为什么连接的时候是三次握手，关闭的时候却是四次挥手？

服务端收到客户端的SYN连接请求报文后，可以直接发送SYN+ACK报文。其中ACK报文是用来应答的，SYN报文是用来同步的。

但是关闭连接时，当服务端收到FIN报文时，很可能并不会立即关闭socket，所以只能先回复一个ACK报文，告诉客户端，“你发的FIN报文，我收到了”。只有等到服务端所有的报文都发送完了，我才能发送FIN报文，因此不能一起发送，故需要四步挥手。

### UDP协议

TCP/IP协议簇中无连接的运输层协议。两部分组成    首部和数据。

### TCP和UDP的区别

1. TCP基于连接，UDP是无连接的；
2. 对系统资源的要求，TCP较多，UDP较少；
3. UDP程序结构较简单；
4. TCP是流模式，而UDP是数据报模式；
5. TCP保证数据正确性，而UDP可能丢包；TCP保证数据顺序，而UDP不保证；

## HTTP请求报文的格式

请求报文：请求行 首部行 实体主体

<img src="https://raw.githubusercontent.com/strutter0816/githubPngImags/main/img/202312062247289.png" alt="img" style="zoom:150%;" />

HTTP响应报文格式  ：状态行 首部行 实体主体

<img src="https://raw.githubusercontent.com/strutter0816/githubPngImags/main/img/202312062249033.png" alt="img" style="zoom:150%;" />

## HTTP请求方法

HTTP请求报文例子中，我们可以看到请求方法是GET，这表示请求读取由URL所标志的信息，除了GET，还有其他几种常用的方法。

![img](https://raw.githubusercontent.com/strutter0816/githubPngImags/main/img/202312062248430.png)

在HTTP响应报文的例子中，我们可以看到状态码是200，表示响应成功。下表是其他状态码，总共5大类，33种。

![img](https://raw.githubusercontent.com/strutter0816/githubPngImags/main/img/202312062249679.png)

## HTTP和HTTPS的区别

HTTP（HyperText Transfer Protocol）和 HTTPS（HyperText Transfer Protocol Secure）是用于在 Web 上传输数据的两种协议，它们之间主要区别在于安全性和数据传输方式。

### HTTP（HyperText Transfer Protocol）:

1. **安全性：** HTTP 不是安全协议，所有的数据传输都是明文的，容易受到中间人攻击，即在数据传输过程中，攻击者可以窃听、修改或篡改传输的数据。
2. **加密：** HTTP 不提供对数据的加密保护机制，因此敏感信息（如用户名和密码）在传输过程中容易被窃取。
3. **端口：** 默认使用端口80进行通信。

### HTTPS（HyperText Transfer Protocol Secure）:

1. **安全性：** HTTPS 是 HTTP 的安全版本。它使用 SSL/TLS 协议对数据进行加密，确保在数据传输过程中的机密性和完整性。
2. **加密：** 通过使用 SSL/TLS，HTTPS 在传输过程中对数据进行加密，防止中间人攻击和窃听。
3. **证书：** 使用数字证书来验证服务器的身份，确保连接的目标是合法的，同时提供对数据传输的身份验证。
4. **端口：** 默认使用端口443进行通信。
5. **性能：** 由于加密和解密需要额外的计算资源，因此 HTTPS 在性能上相对于 HTTP 稍微慢一些，尤其是对于大型网站。

### 区别总结：

- **安全性：** HTTPS比HTTP更安全，适用于对数据保密性和完整性要求较高的场景，如在线支付、用户登录等。
- **加密：** HTTPS通过SSL/TLS协议对传输的数据进行加密，而HTTP传输的数据是明文的。
- **证书：** HTTPS使用数字证书进行服务器和客户端的身份验证，确保连接的安全性。
- **性能：** 由于加密和解密操作的额外开销，HTTPS可能会稍微降低性能，但现代硬件和优化措施可以在很大程度上缓解这个问题。

