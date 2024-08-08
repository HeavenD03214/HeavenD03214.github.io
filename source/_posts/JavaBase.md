
---
title: Java基础
date: 2024-08-07
updated: 
tags:  ["java","多线程","Lambda表达式","stream流","JavaAPI","JVM"]
categories: 基础知识
keywords:
description:
top_img:
comments:
cover:
toc:
toc_number:
toc_style_simple:
copyright:
copyright_author:
copyright_author_href:
copyright_url:
copyright_info:
mathjax:
katex:
aplayer:
highlight_shrink:
aside:
abcjs:

---
# Java基本数据类型

- 基本数据类型：6种数字类型（byte/short/int/long/float/double）、1种字符型（char）、1种布尔型（boolean）
- 引用数据类型：类（Class）、接口（Interface）、数组（Array）
- 除了以上的基本数据类型和引用数据类型，还有一些其他相关的数据类型，例如字符串类型String、枚举类型Enum，它们都是基于引用数据类型来实现的
- **基本数据类型只能存自己类型的值，无其他额外功能**，具体介绍如下第2小节
- 引用类型：参数传递时，以拷贝引用地址的方式传递给接收变量，而非复制整个数据本体。**除八大基本数据类型之外的所有数据类型，都为引用数据类型**。所有引用数据类型的默认值都为null。
- 为了基本数据类型可以与引用数据类型互相转换、以利用彼此的特性，java为每一种基本数据类型提供了相应的包装类。包装类对基本数据类型进行了封装，提供了丰富的功能，**包装类是基本类型的拓展**

## float、double不能用来表示精确的值，运算不精确

解决方案：BigDecimal。创建BigDecimal对象的方式：

- BigDecimal(double val) : double类型的数据作为参数，交给BigDecimal对象【不用，因为double本身不精确】
- BigDecimal(String val) : String类型的数据作为参数，交给BigDecimal对象【用这个】
  注：double->String 直接拼接一个字符串""就行。

## 数据类型转换

转换从低级到高级：byte、short、char（三者同级）——> int ——> long ——> float ——> double

## 基本数据类型与引用数据类型区别

- 存储方式：基本数据类型直接存储值，而引用数据类型存储的是对象的引用（内存地址）
- 内存分配：基本数据类型在栈上分配内存，引用数据类型在堆上分配内存（具体内容存放在堆中，栈中存放的是其具体内容所在内存的地址）。栈上的分配速度较快，但是内存空间较小，而堆上的分配速度较慢，但可以分配更大的内存空间
- 默认值：基本数据类型会有默认值，例如int类型的默认值是0，boolean类型的默认值是false。而引用数据类型的默认值是null，表示没有引用指向任何对象
- 复制操作：基本数据类型进行复制时，会复制该变量的值。而引用数据类型进行复制时，只会复制对象的引用，两个变量指向同一个对象
- 参数传递：基本数据类型作为方法的参数传递时，传递的是值的副本，不会修改原始值。而引用数据类型作为方法的参数传递时，传递的是对象的引用，可以修改对象的属性或状态
- 比较操作：基本数据类型使用==进行比较时，比较的是值是否相等。而引用数据类型使用==进行比较时，比较的是引用是否指向同一个对象，如果要比较对象的内容是否相同，需要使用equals()方法

## 基本数据类型与包装类区别

- 存储方式：基本类型直接存储值，而包装类型存储的是对应基本类型值的对象。
- 空值处理：基本类型没有空值（null）的概念，而包装类型可以将null作为有效值来表示缺失或无效值。
- 默认值：基本类型有默认值，例如int类型的默认值是0，boolean类型的默认值是false。而包装类型的默认值是null。
- 对象操作：基本类型不能直接调用方法，而包装类型可以调用对应的方法，例如Integer类的intValue()方法可以获取保存在Integer对象中的值。
- 自动装箱/拆箱：基本类型和包装类型之间可以进行自动装箱和拆箱的转换。自动装箱是指将基本类型的值自动转换为对应的包装类型对象，如int 转Integer，Integer integer = 100，底层调用了Interger.valueOf(100)方法；而自动拆箱则是将包装类型对象自动转换为基本类型的值。
- 泛型支持：泛型只能使用引用类型，不能直接使用基本类型。因此，当需要在泛型中使用基本类型时，需要使用对应的包装类型。
- 比较方式：基本类型使用==进行比较时，比较的是值是否相等。而包装类型使用==进行比较时，比较的是引用是否指向同一个对象，而不是比较值是否相等。若要比较包装类型的值是否相等，需要使用equals()方法。

# 面向对象(OOP)思想

> 1. 封装（Encapsulation）
>    数据，属性，方法捆绑在一起，成为黑盒。设置访问权限保护数据的完整性，减少错误，增强模块间的独立性。
>
> 2. 继承（Inheritance）
>     继承允许一个类（子类/派生类）继承另一个类（父类/基类）的属性和方法，实现代码的复用。子类可以继承父类的所有非私有属性和方法，并可以增加或重写父类的方法以适应更具体的需求。这有助于建立类的层次结构，促进软件的模块化设计。
>
> 3. 多态（Polymorphism）
>     多态意味着一个接口可以有多种实现方式，或者一个类实例的相同消息可以产生多种响应。在Java等面向对象语言中，多态主要通过方法重写（Override）和接口实现来体现。它使得代码更加灵活和可扩展，因为可以在运行时根据对象的实际类型来决定调用哪个方法，而不是在编译时确定。
>
> 4. 抽象（Abstraction）
>     抽象是指将复杂的系统分解为更简单的组成部分，关注关键特性和行为，忽略不必要的细节。在OOP中，抽象类或接口用来定义一个或多个类的共同属性和操作，但不提供具体实现。抽象类不能被实例化，其目的是为了被子类继承。接口则完全由抽象方法组成，强制实现类遵循某种规范或协议。



# Java内存分区
## 本地内存
> 由操作系统分配和管理的内存区域，它与虚拟机无关。在 Java 中，本地内存通常用于存储 JNI（Java Native Interface）方法调用时的数据以及本地方法库（Native Libraries）等内容。JNI 允许 Java 代码调用本地（非 Java）方法，而本地方法库是由 C、C++ 等语言编写的动态链接库，用于实现这些本地方法。本地内存的分配和释放由操作系统负责管理，而不受 Java 虚拟机的控制。

### 直接内存
> 直接内存是一种特殊的内存缓冲区，并不在 Java 堆或方法区中分配的，而是通过 JNI 的方式在本地内存上分配的。直接内存并不是虚拟机运行时数据区的一部分，也不是虚拟机规范中定义的内存区域，但是这部分内存也被频繁地使用。而且也可能导致 OutOfMemoryError 错误出现。用于提供在堆之外进行对象分配的一种方式。

### 元空间

> 方法区（Method Area）/ 元空间（Metaspace）：
> 方法区是 JVM 运行时数据区域的一块逻辑区域，是各个线程共享的内存区域。方法区会存储已被虚拟机加载的 类信息、字段信息、方法信息、常量、静态变量、即时编译器编译后的代码缓存等数据。
>
> - 需要注意的是，在 JDK 1.8 之后，Java 虚拟机使用元空间（Metaspace）来代替永久代（Permanent Generation）来存储类的元数据。元空间不再位于堆中，而是位于本地内存（Native Memory）中。并且方法区（Method Area）也被替换为元空间（Metaspace）。
> - 方法区和永久代以及元空间的关系？ 
>   - 方法区和永久代以及元空间的关系很像 Java 中接口和类的关系，类实现了接口，这里的类就可以看作是永久代和元空间，接口可以看作是方法区，也就是说永久代以及元空间是 HotSpot 虚拟机对虚拟机规范中方法区的两种实现方式。在 JDK 1.8 之前称为方法区，而在 JDK 1.8 及以后版本使用元空间代替了方法区。
>     运行时常量池：Class 文件中除了有类的版本、字段、方法、接口等描述信息外，还有用于存放编译期生成的各种字面量（Literal）和符号引用（Symbolic Reference）的 常量池表(Constant Pool Table) 。

## 运行时常量池
## 运行时数据
> Java 虚拟机在运行 Java 程序时使用的不同内存区域，由虚拟机动态管理。

### 线程共享
## 堆
> 线程共享的内存区域，用于存储对象实例和数组等动态分配的内存，在虚拟机启动时创建。是 Java 虚拟机管理的最大的一块内存区域，也是垃圾回收的主要区域。
>
> - 字符串常量池：是 JVM 为了提升性能和减少内存消耗针对字符串（String 类）专门开辟的一块区域，主要目的是为了避免字符串的重复创建。HotSpot 虚拟机中字符串常量池保存的是字符串（key）和 字符串对象的引用（value）的映射关系，字符串对象的引用指向堆中的字符串对象。

## 方法区
## 直接内存
> 非运行时数据区的一部分

### 线程私有
## 虚拟机栈
> 线程私有的内存区域，每个线程都有自己的虚拟机栈。用于存储方法执行时的局部变量、操作数栈、动态链接、方法出口等信息。方法调用的数据需要通过栈进行传递，每一次方法调用都会有一个对应的栈帧被压入栈中，方法调用结束后，栈帧被弹出。局部变量放在栈里面，形参属于局部变量。而成员变量随着类的创建而产生，放在堆里面。
>
> - 局部变量表：主要存放了编译期可知的各种数据类型（boolean、byte、char、short、int、float、long、double）、对象引用（reference 类型，它不同于对象本身，可能是一个指向对象起始地址的引用指针，也可能是指向一个代表对象的句柄或其他与此对象相关的位置）。
> - 操作数栈：主要作为方法调用的中转站使用，用于存放方法执行过程中产生的中间计算结果。另外，计算过程中产生的临时变量也会放在操作数栈中。
> - 动态链接：主要服务一个方法需要调用其他方法的场景。Class 文件的常量池里保存有大量的符号引用比如方法引用的符号引用。当一个方法要调用其他方法，需要将常量池中指向方法的符号引用转化为其在内存地址中的直接引用。动态链接的作用就是为了将符号引用转换为调用方法的直接引用，这个过程也被称为 动态连接 。
> - 方法出口：Java 方法有两种返回方式，一种是 return 语句正常返回，一种是抛出异常。不管哪种返回方式，都会导致栈帧被弹出。也就是说， 栈帧随着方法调用而创建，随着方法结束而销毁。无论方法正常完成还是异常完成都算作方法结束。
>   除了 StackOverFlowError 错误之外，栈还可能会出现OutOfMemoryError错误，这是因为如果栈的内存大小可以动态扩展， 如果虚拟机在动态扩展栈时无法申请到足够的内存空间，则抛出OutOfMemoryError异常。

## 本地方法栈
> 类似于虚拟机栈，但是用于执行本地方法（Native Method）的线程私有内存区域。
> 存储本地方法的局部变量、操作数栈、动态链接等信息。

## 程序计数器
> 线程私有的内存区域，每个线程都有一个程序计数器。
> 主要用于记录当前线程正在执行的字节码指令的地址或者正在执行的方法的当前行号。字节码解释器通过改变程序计数器来依次读取指令，从而实现代码的流程控制，如：顺序执行、选择、循环、异常处理。
> 在线程切换时，程序计数器是不会发生线程间切换的，每个线程都会有独立的计数器记录执行位置。当线程被切换回来的时候能够知道该线程上次运行到哪儿了。
> ⚠️ 注意：程序计数器是唯一一个不会出现 OutOfMemoryError 的内存区域，它的生命周期随着线程的创建而创建，随着线程的结束死亡。



# Java内存回收算法



# 常用Java Api

## String、StringBuffer和 StringBuilder

> 为什么拼接、反转字符串的时候要用StringBuilder？
>
> String：内容不可变、拼接字符串性能差‘
>
> StringBuilder：内容是可变的、拼接字符串性能好、书写优雅
>
> 定义字符串使用String；
>
> 拼接、修改等操作字符串使用StringBuilder。

## BigDecimal

### BigDecimal与MySQL的映射关系

> 在MySQL中，我们可以使用DECIMAL数据类型来存储高精度的数值。DECIMAL类型可以指定精度和小数位数，因此非常适合存储BigDecimal类型的数据。在Java中，我们可以使用BigDecimal的构造方法将DECIMAL类型的数据转换为BigDecimal对象，也可以使用BigDecimal的toString方法将BigDecimal对象转换为DECIMAL类型的字符串。

### 注意事项
【强制】 禁止使用构造方法BigDecimal(double) 的方式把 double 值转化为 BigDecimal 对象。

 说明：BigDecimal(double) 存在精度损失风险，在精确计算或值比较的场景中可能会导致业务逻辑异常。

 如：BigDecimal g = new BigDecimal(0.1F); 实际的存储值为：0.10000000149。

 正例： 优先推荐入参为 String 的构造方法，或使用 BigDecimal 的 valueOf 方法，此方法内部其实执行了 Double 的 toString，而 Double 的 toString 按 double 的实际能表达的精度对尾数进行了截断

# Java多线程

## 创建线程的方式

> 本质都是基于Runnable接口的方式来创建的

### 1.继承Thread类

```java
public class xxx extend Thread{
    @Override
    pulic void run(){
        ……
    }
     public static void main(String[] args){
        Thread thread = new xxx(new xxx());
        thread.start();
    }
}
```

### 2.实现Runnable接口

```java
public class xxx implements Runnable{
    @Override
    pulic void run(){
        ……
    }
    
    public static void main(String[] args){
        Thread thread = new Thread(new xxx());
        thread.start();
    }
}
```

可以使用匿名内部类或Lambda表达式的方式

## 匿名内部类

```java
new Thread(new Runnable(){
	@Override
	pulic void run(){
        ……
    }
}).start();
```

## Lambda表达式

参数是接口实现实例且接口只需要实现一个方法（函数式接口）

```java
new Thread(()->{
	……
}).start();
```

### 3.实现Callable接口

```java
import java.util.concurrent.Callable;
import java.util.concurrent.FutureTask;
 
public class CallableExample implements Callable<String> {
    @Override
    public String call() throws Exception {
        // 这里是任务的代码
        return "任务执行完毕";
    }
 
    public static void main(String[] args) {
        Callable<String> callable = new CallableExample();
        FutureTask<String> futureTask = new FutureTask<>(callable);
 
        new Thread(futureTask).start();
 
        try {
            // 获取callable任务的返回值
            String result = futureTask.get();
            System.out.println(result);
        } catch (InterruptedException | ExecutionException e) {
            e.printStackTrace();
        }
    }
}
```

### 4.利用线程池创建

```java
public class xxx implements Runnable{
    @Override
    pulic void run(){
        ……
    }
    
    public static void main(String[] args) throws ExecutionException ...{
        ExecutorService executorService = Executors.newFixedThreadPool(10);
        executorService.execute(new XushuThread());
    }
}
```

### 5.匿名内部类/6.Lambda表达式

- Runnable接口是函数式接口



## 线程操作

### 为什么不推荐用Excutores创建线程池

```java
//存在阻塞队列，最大值为Interger.MAX_VALUE，高并发情况下阻塞队列中等待任务过多会造成OOM
newFixedThreadPool() //指定线程创建数量
newSingleThreadExecutor() //固定只创建一个线程
//动态扩容，最大线程数是Interger.MAX_VALUE，高并发情况下阻塞队列中等待任务过多会造成OOM
newCachedThreadPool()
//推荐使用：
    new ThreadPoolExecutor(参数如下)
```

### 参数说明

```java
corePoolSize 核心线程数量
maximumPoolSize 最大线程数量
keepAliveTime 非核心线程的空闲状态的存活时间
unit 时间单位
workQueue 工作队列（阻塞队列）
threadFactory 线程工厂(创建线程)
handler 拒绝策略
```

### 提交流程
```mermaid
---
title: 提交流程
---
flowchart LR
  submit=>start: 提交任务
  coremax=>condition: 核心线程是否已满
  queuemax=>condition: 阻塞队列是否已满
  threadmax=>condition: 是否已达到最大线程数
  reject=>end: 拒绝策略
  core=>operation: 创建核心线程，执行任务
  queue=>operation: 加入到阻塞队列中排队
  temp=>operation: 创建临时线程，执行任务(设置keepAliveTime)
  submit->coremax
  coremax(yes)->queuemax
  coremax(no)->core
  queuemax(yes)->threadmax
  queuemax(no)->queue
  threadmax(yes)->reject
  threadmax(no)->temp
```



### 执行流程

- 执行任务的run方法

- 任务执行完从阻塞队列中拿任务getTask()
- getTask()

- 通过当前线程数是否大于核心线程数来判断是否为核心线程

```java
workQueue.poll(keppAliveTime, TimeUnit.NANOSECONDS) : //阻塞存活时间拿取任务   ---临时线程
work Queue.take()；//阻塞无限时间拿取任务 ---核心线程
```

- 临时线程在存活时间内拿不到任务执行就会执行

```java
compareAndDecrementWorkerCount(int expect){  //销毁线程
    //通过CAS方式将进程数-1，保证同一时间只有一个线程执行线程数-1操作
    return ctl.compareAndSet(expect, exect-1);
    //通过CAS销毁
    //线程会随机减少一个
    //线程池并没有严格的标志某一个线程一定是核心线程
}    
```

### 线程异常中断

任务执行报错就会抛出异常，线程处理时会捕获并抛出，线程抛出异常就会导致线程中断销毁

- 为什么不忽略任务，直接执行下一个
  - 一般任务执行失败都需要进行相关失败处理
  - 线程池中可以设置一个异常捕获处理

### 线程关闭

```java
A： threadPool.shutdown();||
B： threadPool.shutdownNow();
```

- 两种方法调用时会改变线程池状态，A-SHUTDOWN，B-STOP（在判断时会直接return null,销毁线程）
- 此时就无法提交任务（直接将任务派给核心线程或将任务塞入阻塞队列），因为会判断线程池处于运行状态
- 线程在执行任务时被通知关闭通过，thread.interrupt() 
- 线程执行拿任务过程中被通知关闭，即阻塞拿任务时，会触发InterruptedException异常，将timeout设置为false
- 线程刚刚拿到任务被通知要关闭，会将任务执行完后再在拿取任务时被关闭(return null)

## 锁

### Sychroized

> Java中的一个关键字
>
> JVM层面
>
> 自动加锁和释放锁
>
> 不可获取当前线程是否上锁
>
> 非公平锁
>
> 不可中断
>
> 锁的是对象，锁信息保存在对象头中
>
> - 底层有锁升级过程
>   - 无锁=>偏向锁=>轻量级锁=>重量级锁

## 锁升级过程

> 通过并发量，动态调节锁的实现

- 偏向锁，在锁对象对象头中记录当前获取到该锁的线程id，该线程下次如果又来获取该锁就可以直接获取到，也就是支持锁重入

- 轻量级锁：两个或以上线程交替获取锁，但并没有在对象上并发的获取锁时，偏向锁会升级成轻量级锁。

  - 此阶段线程采用CAS自旋方式尝试获取锁，避免阻塞线程造成的cpu在用户态和内核态间转换的消耗

- 重量级锁：两个或以上线程并发的在同一个对象上进行同步时，为了避免无用自旋消耗cpu，轻量级锁会升级成重量级锁

- 自旋锁：

  

### ReentrantLock

> JDK提供的一个类
>
> API层面的锁
>
> 需要手动加锁与释放锁
>
> 可获取当前线程是否上锁（isHeldByCurrentThread）
>
> - 公平锁或非公平锁 new ReentrantLock(true || false)
>
> - 可中断
>
> ```java
> //1.设置超时方法
> tryLock(long timeout,timeUnit unit);
> //2.调用lockInterruptibly()放到代码块中
> //后调用interrupt()方法可以中断
> ```
>
> int类型的state标识来标识锁的状态
>
> 没有锁升级过程

## 公共锁和非公平锁

> 只体现在加锁阶段，对线程被唤醒阶段没有影响

- 公平锁会检查AQS队列中是否存在线程在排队，如果有排队则当前线程也进行排队
- 非公平锁不会去检查是否有线程排队，直接去竞争锁资源，如果没有竞争到则也进行排队

## ThreadLocal

线程本地存储机制，利用该机制将数据缓存在某个线程内部，该线程可以在任意时刻，任意方法中获取缓存的数据

- 本质是暴露出来用来操作当前线程的ThreadLocalMap的工具类

- ThreadLocalMap存储Entry（键值对）对象，其中键为ThreadLocal值为缓存的数据

### 内存泄漏

- ThreadLocal对象使用完后应该对Entry对象进行手动回收（ThreadLocal的remove方法）

- 线程通过强引用指向ThreadLocalMap，ThreadLocalMap又通过强引用指向Entry，所以线程不被回收，Entry对象也就不会回收

### 应用场景 

> 共享变量，但每个线程互不影响，相互隔离，就可以使用ThreadLocal

- a:  跨层传递信息，每个方法调用都要声明重复参数，存储ThreadLocal中，即可省去传参直接全局调用
- b：隔离线程，存储一些线程不安全的工具对象，如（SimpleDateFormat）
- c:  Spring的事务管理器
- d:  springmvc实现线程安全
  - springmvc的HttpSession、HttpServletReuquest、HttpServletResponse，servlet是单例的
  - springmvc允许在controller类中通过@Autowired配置request，response，requestcontext等实例对象

## Tomcat为什么要自定义类加载器

一个 T omcat 中可以部署多个应用，而每个应用中都存在很多类，并且各个应用中的类是独立的全类名是可以相同的，比如一个订单系统中可能存在 com .xushu.User 类，一个库存系统中可能也存在 com.xushu.User类 ，一个 Tomcat, 不管内部部署了多少应用， Tomcat 启动之后就是一个Javai程，也就是一个 JVM ，所以如果 Tomcat 中只存在一个类加载器，比如默认的AppClassLoader, 那么就只能加 载一 个 com.xushu.User类 ，这是有问题的，而在 Tomcat 中，为部署的每个应用都生成一个类加载器实例，名字叫做 WebAppClassLoader, 这样 Tomcat 中每个应用就可以使用自己的类加载器去加载自己的类，从而达到应用之间的类隔离，不出现冲突。另外 Tomcat 还利用自定义加载器实现了热加载功能·

# Lambda表达式

语法糖，简化某些匿名内部类的写法

## 基本格式

```
(参数列表)->{代码}
```

## 举例

### 匿名内部类

```java
new Thread(new Runnable(){
	@Override
	pulic void run(){
        ……
    }
}).start();
```

### Lambda表达式

调用的方法参数是接口实现实例且接口只有有一个抽象方法（函数式接口）

> 1.参数类型可推导可省略类型声明
>
> 2.只有一个参数可省略括号
>
> 3.实现只有一行代码可省略大括号，如果一行代码包括return可以把return也省略
>
> 4.省略上述，编译器里用快捷键alt + enter

```java
new Thread(()->{
	……
}).start();
```

# Stream流

Java8新特性，使用函数式编程，可以使对数组和集合进行链状流式操作更加方便

- 惰性求值，没有终结操作不执行
- 流是一次性的，执行完释放
- 不会影响原数据

## 快速入门

```java
数组和集合.stream()
    		//去重(类中一般需要重写equals 和 hashcode)
            .distinct() 
    		//条件过滤参数是函数式接口
            .filter((需要筛除的对象类型参数) ->{
            //筛出规则
            })   
    		 //循环遍历参数是函数式接口
    		.forEach((需要操作的对象类型参数) -> {
             //需求操作
            })
```

### 创建流

## 单列集合

```java
集合对象.stream()
```

## 数组

```java
Arrays.stream(数组) || Stream.of(数组)
```

## 双列集合

//将键值对封装成Entry对象后再创建流对象

```java
map.entrySet().Stream()
```

### 中间操作

- filter 重写过滤条件（返回true / false）过滤数据

  - ```
    .filter(author -> author.getAge() > 18)
    ```

    

- map 对流中的元素进行计算或转换

  - ```java
    创建流对象
    	.map(元素对象 -> 对象.get属性()) //只需要对对象中的某个属性进行操作
        
        重写了的接口function为:
    new Fuction<对象类型, Object>() {
        @Override
        public Object apply(对象类型 参数){
            //对属性进行操作
            //返回需要的属性
        }
    }
    ```

- flatMap

  - 把一个对象转换成多个对象作为流中的元素，

  - ```java
    //一个作家多本书，使用map转换出来的对象是List集合，遍历操作需要嵌套遍历
    //flatmap则把书列表转换成流然后拼接，这样就得到了所有的书，遍历时也无需嵌套了
    .flatMap(author -> author.getBooks().stream()) //此时得到所有书的对象流
        //如果想得到书的标签，但标签是一个长字符串如 “爱情,玄幻”
        //使用split分割字符串成数组再转换成流
    .flatMap(book -> Arrays.stream(book.getTags().split(","))
    ```

    

- distinct 去重，依赖Object的equals方法来判断(类中一般需要重写equals 和 hashcode)

- sorted 对流中的元素进行排序

  - 类里实现Comparable接口（频繁调用）

  - 匿名内部类 => Lambda表达式（特殊调用）

  - ```java
    .sorted((o1, o2) -> o2.getAge() - o1.getAge())
        
      //重写Comparator接口的Compare方法
        public int compare (Author o1, Author o2){
        	return o2.getAge() - o1.getAge();
    }
        
    ```

- limit 设置流的最大长度，超出部分将会抛弃

  - ```
    .limit(int)
    ```

- skip 跳过流当中的前n个元素，返回剩下的元素

  - ```
    .skip(int)
    ```

### 终结操作

- forEach() 遍历流中对象并进行相关操作

  - ```java
    .forEach(对象 -> 操作)
    ```

- count 获取当前流中元素的个数

  - ```java
    .count();
    ```

- max & min

  - ```java
    //相当于sort + limit
    //需要重写比较器的compare方法
    .max((score1, score2) -> score1 - score2);
    ```

- collect 把流当中的元素转化成集合

  - ```java
    //list
    .collect(Collectors.toList())
    //set
    .collect(Collectors.toSet())
    //map
    .collect(Collectors.toMap(author -> author.getName(), author -> author.getBookList()))
    ```

- anyMatch

  - ```java
    //同filter过滤器一样，参数为实现Predicate接口
    //只要有一个满足条件返回true
    .anyMatch(author -> author.getAge() > 29)
    ```

- allMatch

  - ```java
    //同filter过滤器一样，参数为实现Predicate接口
    //所有对象均符合条件返回true
    .allMatch(author -> author.getAge() > 29)
    ```

- noneMatch

  - ```java
    //同filter过滤器一样，参数为实现Predicate接口
    //所有对象均不符合条件返回true
    .noneMatch(author -> author.getAge() > 29）
    ```

- findAny

  - ```java
    //同filter过滤器一样，参数为实现Predicate接口
    //获取任意一个符合条件的对象
    .findAny(author -> author.getAge() > 29)
    ```

- findFirst

  - ```java
    //同filter过滤器一样，参数为实现Predicate接口
    //获取第一个符合条件的对象
    .findAny(author -> author.getAge() > 29)
    ```

- reduce 归并 ，对流中的数据按照指定计算方式计算出一个结果

  - ```
    //使用reduce求年龄和
    .map(author -> author.getAge())
    .reduce(0, (result, elment) -> result + element)
    ```

  - ```
    //使用reduce求年龄最大值,最小值同理
    .map(author -> author.getAge())
    .reduce(Interger.MIN_VALUE, (result, elment) -> result < element ? element : result)
    ```



## Optional

### 创建对象

- ```java
  Author author = getAuthor(); //实际上期望getAuthor()的返回值就是Optional，进行提前封装
  Optional<Author> authorOptional = Optional.ofNullable(author);
  authorOptional.ifPresent(author -> {
  	//具体操作
  })
  //确定author对象非空
  则可以用
  Optional.of(author);
  //创建空对象
  Optional.empty);
  ```

### 安全获取值

```java
author.orElseGet(() -> new Author()); //不为空返回author，为空返回默认值new Author()

//如果期望抛出异常，使用后端框架进行统一异常捕获
author.orElseThrow(() -> new RuntimeException("")); //不为空返回author，为空返回默认值new Author()
```

### 过滤

- 使用.filter()同前面的中间操作一样,返回值是过滤后的Optional<T>

### 判断

- 除去ifpresent（函数式接口传参）外还有一个isPresent需要用if else判断不够优雅

### 数据转换

- 使用.map()同前面的中间操作一样,返回值是过滤后的Optional<T>



## 函数式接口

接口当中只有一个抽象方法（一般都有@FunctionalInterface注解）



## 方法引用

- 基本格式： 类名或对象名::方法名

### 引用类的静态方法

```java
.map(author -> author.getAge())
.map(age -> String.valueof(age))
//可以转化成
.map(author -> author.getAge())
    //重写方法仅一行代码，使用某个类的静态方法，且所有参数都传入该静态方法
.map(String::valueOf)
```

### 引用对象的实例方法

- 重写方法仅一行代码，使用某个实例对象的方法，且所有参数都传入该方法
  - 该对象::方法名

### 引用类的实例方法

- 重写方法仅一行代码，使用第一个参数的成员方法，且其它所有参数都传入该方法
  - 该成员对象::方法名

```java
.map(author -> author.getAge())
//可以转化成
.map(author::getAge)
```

### 构造器引用

- 重写方法仅一行代码，使用某个类的构造器，且所有参数都传入该构造器
  - 该类名::new

```java
.map(author -> new StringBuilder(author))
//可以转化成
.map(StringBuilder::new)
```

## 高级用法

### 基本数据类型优化

- 使用基本数据类型包装类进行操作时会进行不断地自动拆箱装箱，数据量大时会消耗很多时间

```
.map(author -> author.getAge()) //Interger类型
.map(age -> age + 10) //int基本类型操作，先拆箱后装箱
//转换成
.mapToInt(author -> author.getAge()) //int类型
.map(age -> age + 10) //int基本类型操作，无需拆箱装箱
```

## 并行流

- 多线程执行流操作  

```java
.parallerl() //成为并行流对象
    .peek(num -> Sysytem.out.println(num + Thread.currenThread().getName()))  //调试方法，中间操作
```



# 引用方法

## 强引用 (Strong Reference)

这是最常用的引用类型。当一个对象被强引用关联时，只要这个引用存在，垃圾收集器就不会回收这个对象。
实例化一个对象并将其赋值给一个变量时，这个变量就是一个强引用。
只有当没有强引用指向一个对象，并且该对象不可达时，垃圾收集器才可能回收它。

## 软引用 (Soft Reference)

软引用是用来描述那些有用但不是必须的对象。在系统将要发生内存溢出异常前，会把这些对象列进回收范围之中进行第二次回收。
如果使用软引用来保存一个对象，只要内存足够，对象就不会被回收。
软引用通常用于实现内存敏感的缓存，例如图像缓存或数据库结果集缓存。

【1】软引用 (Soft Reference)实例
软引用（Soft Reference）在Java中主要用于实现内存敏感的缓存。当Java虚拟机（JVM）的内存开始变得紧张时，软引用指向的对象可能会被垃圾回收器回收，从而释放内存空间。软引用通常与引用队列（Reference Queue）结合使用，以便在软引用对象被垃圾回收器回收时接收到通知。

下面是一个使用SoftReference的简单示例，展示了如何创建软引用并检查对象是否仍然可达：



```java
import java.lang.ref.SoftReference;
import java.lang.ref.ReferenceQueue;
import java.lang.ref.Reference;

public class SoftReferenceExample {
    public static void main(String[] args) {
        // 创建一个引用队列
        ReferenceQueue<String> queue = new ReferenceQueue<>();
        // 创建一个字符串对象，并使用软引用指向它
        String str = new String("Hello, SoftReference!");
        SoftReference<String> softRef = new SoftReference<>(str, queue);

        // 检查软引用是否仍然指向一个可达对象
        System.out.println("Initially: " + softRef.get());  // 输出: Hello, SoftReference!

        // 尝试手动回收垃圾（这通常不会立即导致软引用对象被回收）
        System.gc();

        // 等待一段时间，让JVM有机会执行垃圾回收
        try {
            Thread.sleep(500);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        // 再次检查软引用是否仍然指向一个可达对象
        System.out.println("After GC: " + softRef.get());  
        // 输出可能还是: Hello, SoftReference!，除非内存真的紧张

        // 手动设置原始引用为null，使对象仅由软引用持有
        str = null;

        // 再次尝试垃圾回收
        System.gc();

        // 等待一段时间，让JVM有机会执行垃圾回收
        try {
            Thread.sleep(500);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        // 最后检查软引用是否仍然指向一个可达对象
        System.out.println("Finally: " + softRef.get());  // 输出可能是: null，表示对象已被回收
        }
}
```
创建了一个SoftReference来指向一个字符串对象。

尝试调用System.gc()来请求垃圾回收。

请注意，System.gc()只是一个提示，JVM并不保证会立即执行垃圾回收。使用Thread.sleep()来等待一段时间，给JVM一个执行垃圾回收的机会。

最后，将原始的强引用设置为null，这意味着只有软引用在维持着对象的生命。再次请求垃圾回收后，如果此时JVM认为有必要释放更多内存，软引用指向的对象就可能被回收。

在实际应用中，软引用通常用于缓存场景，例如缓存图像、文件或计算结果，这样在内存压力增加时，这些缓存项可以被释放，避免程序因内存不足而崩溃。

## 弱引用 (Weak Reference)

弱引用的强度比软引用更低。在下一次垃圾收集发生时，不管系统内存是否充足，弱引用都会被回收。
弱引用对象在下一次垃圾收集时一定会被回收，即使系统中还有足够的内存。
弱引用通常用于实现快速失败的缓存或辅助清理操作，如ThreadLocal的清理。

【2】弱引用 (Weak Reference)实例

弱引用（Weak Reference）在Java中用于创建那些在下一次垃圾回收时一定会被回收的对象引用。弱引用比软引用更弱，它不提供任何关于对象生存时间的保证，只要垃圾回收器运行，弱引用指向的对象就会被回收。

下面是一个使用WeakReference的示例，展示如何创建弱引用以及如何检测对象是否仍然可达：


​        
```java
import java.lang.ref.WeakReference;
import java.lang.ref.ReferenceQueue;
import java.lang.ref.Reference;

public class WeakReferenceExample {
    public static void main(String[] args) {
        // 创建一个引用队列
        ReferenceQueue<String> queue = new ReferenceQueue<>();
   
        // 创建一个字符串对象，并使用弱引用指向它
        String str = new String("Hello, WeakReference!");
        WeakReference<String> weakRef = new WeakReference<>(str, queue);

        // 检查弱引用是否仍然指向一个可达对象
        System.out.println("Initially: " + weakRef.get());  // 输出: Hello, WeakReference!

        // 手动设置原始引用为null，使对象仅由弱引用持有
        str = null;

        // 强制垃圾回收
        System.gc();

        // 等待一段时间，让JVM有机会执行垃圾回收
        try {
            Thread.sleep(500);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        // 检查弱引用是否仍然指向一个可达对象
        System.out.println("After GC: " + weakRef.get());  // 输出可能是: null，表示对象已被回收

        // 检查引用队列是否已经收到了弱引用的通知
        Reference<? extends String> ref = (Reference<? extends String>)queue.poll();
        if (ref != null) {
            System.out.println("Reference was enqueued.");
        }
    }
}
```
在这个示例中，我们首先创建了一个WeakReference对象weakRef，它指向一个字符串对象。然后，我们将原始的强引用str设置为null，这意味着现在只有弱引用在维持着对象的生命。

接下来，我们调用System.gc()来强制垃圾回收。由于弱引用的特点，即使系统内存充足，弱引用指向的对象也会在垃圾回收时被回收。我们使用Thread.sleep()来等待一段时间，确保垃圾回收有机会被执行。

最后，我们检查弱引用weakRef是否仍然指向一个可达对象。如果对象已经被垃圾回收器回收，get()方法将返回null。

此外，我们还使用了引用队列（ReferenceQueue），当弱引用的对象被垃圾回收器回收后，弱引用会被加入到队列中。我们可以通过poll()方法从队列中取出引用，确认对象已经被回收。

弱引用通常用于实现线程局部变量（ThreadLocal）的自动清理功能，或者用于创建不需要长时间存在的对象的缓存。当对象不再被任何强引用持有时，弱引用允许这些对象迅速被垃圾回收器回收，从而节省内存。

## 幻象引用 (Phantom Reference 或 虚引用)

幻象引用是最弱的一种引用关系，一个对象是否有幻象引用的存在完全不会对其生存时间构成影响，也无法通过幻象引用来获取一个实例。
幻象引用的用途是在对象被垃圾收集器回收之后收到一个系统通知，类似于“finalization”机制，但是更加灵活和可控。
它们需要与ReferenceQueue配合使用，以接收引用被垃圾收集器清理的通知

【3】幻象引用 (Phantom Reference 或 虚引用)实例
幻象引用（Phantom Reference），也被称为虚引用，是Java中引用类型中最弱的一种。幻象引用不能单独使用来访问对象，它的主要作用是在对象被垃圾回收器回收时收到一个系统通知。幻象引用总是与引用队列（ReferenceQueue）一起使用，当引用所指向的对象被回收时，这个引用会被加入到引用队列中。

下面是一个使用PhantomReference的示例，展示如何创建幻象引用以及如何检测对象是否已经被垃圾回收器回收：

```java
import java.lang.ref.PhantomReference;
import java.lang.ref.ReferenceQueue;
import java.lang.ref.Reference;

public class PhantomReferenceExample {
    public static void main(String[] args) {
        // 创建一个引用队列
        ReferenceQueue<Object> queue = new ReferenceQueue<>();
        
        // 创建一个对象
        Object obj = new Object();
        
        // 使用幻象引用指向这个对象，注意构造函数的第二个参数是引用队列
        PhantomReference<Object> phantomRef = new PhantomReference<>(obj, queue);

        // 此时，直接通过幻象引用无法获取到对象，因为幻象引用本身并不能保持对象的可达性
        System.out.println("Before GC: " + phantomRef.get());  // 输出: null

        // 手动设置原始引用为null，使对象仅由幻象引用持有
        obj = null;

        // 强制垃圾回收
        System.gc();

        // 等待一段时间，让JVM有机会执行垃圾回收
        try {
            Thread.sleep(500);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        // 检查引用队列，看是否已经收到了幻象引用的通知
        Reference<?> ref = queue.poll();
        if (ref != null) {
            System.out.println("Phantom reference was enqueued after object was garbage collected.");
        }
        
        // 再次尝试通过幻象引用获取对象，应该仍然是null
        System.out.println("After GC: " + phantomRef.get());  // 输出: null
    }
}

```

在这个示例中，我们首先创建了一个引用队列queue。接着，我们创建了一个普通的Java对象obj，然后使用PhantomReference创建了一个指向该对象的幻象引用phantomRef，并将引用队列作为构造函数的参数传入。

当我们尝试通过幻象引用phantomRef.get()来获取对象时，会发现返回的是null。这是因为幻象引用本身并不能保持对象的可达性，它不会阻止垃圾回收器回收这个对象。

然后，我们将原始的强引用obj设置为null，这意味着现在没有任何强引用指向这个对象，它将变为垃圾。我们调用System.gc()来强制垃圾回收，并使用Thread.sleep()来等待一段时间，确保垃圾回收有机会被执行。

最后，我们检查引用队列queue，如果幻象引用phantomRef所指向的对象已经被垃圾回收器回收，那么phantomRef会被加入到引用队列中。我们可以通过poll()方法从队列中取出引用，确认对象已经被回收。

幻象引用的主要应用场景是在对象被垃圾回收器回收之后，进行一些必要的清理工作，例如关闭资源、更新数据库状态等。由于幻象引用本身无法保持对象的可达性，因此它不能用于对象的访问，只能用于监听对象的销毁事件。
