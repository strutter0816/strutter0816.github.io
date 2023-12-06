# 面向对象编程


<!--more-->

## 三大特性

- 封装

  利用抽象数据类型将数据和基于数据的操作封装在一起，使其构成一个不可分割的独立实体。数据被保护在抽象数据类型的内部，尽可能地隐藏内部的细节，只保留一些对外的接口使其与外部发生联系。用户无需关心对象内部的细节，但可以通过对象对外提供的接口来访问该对象。

- 继承

  is-a的关系 继承关系，例如 Cat 和 Animal 就是一种 IS-A 关系，因此 Cat 可以继承自 Animal，从而获得 Animal 非 private 的属性和方法。

  >is-a/has--a/like-a
  >
  >- is-a 继承关系 A is a B 说明A是B的一个子类
  >- has-a 表示从属关系A has a B，那么B就是A的组成部分。 同一种类的对象，通过它们的属性的不同值来区别。
  >- like-a，顾名思义，像一个，代表组合关系。 如果A like a B，那么B就是A的接口。

  Cat 可以当做 Animal 来使用，也就是说可以使用 Animal 引用 Cat 对象。父类引用指向子类对象称为 **向上转型** 。

  ```java
  Animal animal = new Cat();
  ```

- 多态

  多态分为编译时多态和运行时多态：

  - 编译时多态主要指方法的重载
  - 运行时多态指程序中定义的对象引用所指向的具体类型在运行期间才确定

  运行时多态有三个条件：

  - 继承

  - 覆盖（重写）

  - 向上转型

    下面的代码中，乐器类（Instrument）有两个子类：Wind 和 Percussion，它们都覆盖了父类的 play() 方法，并且在 main() 方法中使用父类 Instrument 来引用 Wind 和 Percussion 对象。在 Instrument 引用调用 play() 方法时，会执行实际引用对象所在类的 play() 方法，而不是 Instrument 类的方法。

    ```java
    public class Instrument {
    
        public void play() {
            System.out.println("Instument is playing...");
        }
    }
    public class Wind extends Instrument {
    
        public void play() {
            System.out.println("Wind is playing...");
        }
    }
    public class Percussion extends Instrument {
    
        public void play() {
            System.out.println("Percussion is playing...");
        }
    }
    public class Music {
    
        public static void main(String[] args) {
            List<Instrument> instruments = new ArrayList<>();
            instruments.add(new Wind());
            instruments.add(new Percussion());
            for(Instrument instrument : instruments) {
                instrument.play();
            }
        }
    }
    Wind is playing...
    Percussion is playing.
    ```

## 类图

### 泛化关系

用来描述继承关系，在 Java 中使用 extends 关键字。

![img](https://raw.githubusercontent.com/strutter0816/githubPngImags/main/img/202312062246134.jpeg)

### 实现关系

用来实现一个接口，在 Java 中使用 implements 关键字。

![img](https://raw.githubusercontent.com/strutter0816/githubPngImags/main/img/202312062246998.jpeg)

### 聚合关系

表示整体由部分组成，但是整体和部分不是强依赖的，整体不存在了部分还是会存在。

![img](https://raw.githubusercontent.com/strutter0816/githubPngImags/main/img/202312062246648.jpeg)

### 组合关系

和聚合不同，组合中整体和部分是强依赖的，整体不存在了部分也不存在了。比如公司和部门，公司没了部门就不存在了。但是公司和员工就属于聚合关系了，因为公司没了员工还在。

### 关联关系

表示不同类对象之间有关联，这是一种静态关系，与运行过程的状态无关，在最开始就可以确定。因此也可以用 1 对 1、多对 1、多对多这种关联关系来表示。比如学生和学校就是一种关联关系，一个学校可以有很多学生，但是一个学生只属于一个学校，因此这是一种多对一的关系，在运行开始之前就可以确定。

### 依赖关系

和关联关系不同的是，依赖关系是在运行过程中起作用的。A 类和 B 类是依赖关系主要有三种形式：

- A 类是 B 类方法的局部变量；
- A 类是 B 类方法的参数；
- A 类向 B 类发送消息，从而影响 B 类发生变化。

## 设计原则

| 简写 |                全拼                 |   中文翻译   |
| :--: | :---------------------------------: | :----------: |
| SRP  | The Single Responsibility Principle | 单一责任原则 |
| OCP  |      The Open Closed Principle      | 开放封闭原则 |
| LSP  |  The Liskov Substitution Principle  | 里氏替换原则 |
| ISP  | The Interface Segregation Principle | 接口分离原则 |
| DIP  | The Dependency Inversion Principle  | 依赖倒置原则 |

#### 单一责任原则

> 修改一个类的原因应该只有一个。

换句话说就是让一个类只负责一件事，当这个类需要做过多事情的时候，就需要分解这个类。

如果一个类承担的职责过多，就等于把这些职责耦合在了一起，一个职责的变化可能会削弱这个类完成其它职责的能力。

#### 开放封闭原则

> 类应该对扩展开放，对修改关闭。

扩展就是添加新功能的意思，因此该原则要求在添加新功能时不需要修改代码。

符合开闭原则最典型的设计模式是装饰者模式，它可以动态地将责任附加到对象上，而不用去修改类的代码。

#### 3. 里氏替换原则

> 子类对象必须能够替换掉所有父类对象。

继承是一种 IS-A 关系，子类需要能够当成父类来使用，并且需要比父类更特殊。

如果不满足这个原则，那么各个子类的行为上就会有很大差异，增加继承体系的复杂度。

#### 4. 接口分离原则

> 不应该强迫客户依赖于它们不用的方法。

因此使用多个专门的接口比使用单一的总接口要好。

#### 5. 依赖倒置原则

> 高层模块不应该依赖于低层模块，二者都应该依赖于抽象；
> 抽象不应该依赖于细节，细节应该依赖于抽象。

高层模块包含一个应用程序中重要的策略选择和业务模块，如果高层模块依赖于低层模块，那么低层模块的改动就会直接影响到高层模块，从而迫使高层模块也需要改动。

