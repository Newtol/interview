# JVM知识点总结

[TOC]

## 1. JVM、JDK和JRE关系

+ JVM：就是我们常说的**Java虚拟机**，它是整个java实现跨平台的最核心的部分，所有的java程序会首先被编译为.class的类文件，这种类文件可以在虚拟机上执行，也就是说class并不直接与机器的操作系统相对应，而是经过虚拟机间接与操作系统交互，由虚拟机将程序解释给本地系统执行。

+ JRE：**Java 运行环境**。它主要包含两个部分：JVM 的标准实现和 Java 的一些基本类库。相对于 JVM 来说，JRE多出来一部分 Java 类库。
+ JDK：**Java开发工具包**，在其安装目录下面有六个文件夹、一些描述文件、一个src压缩文件。bin、include、lib、 jre这四个文件夹起作用，demo、sample是一些例子。
  + bin：最重要的是编译工具（javac.exe）
  + include：java和JVM交互用的头文件
  + lib：类库
  + jre：Java运行环境（即安装了JDK，就不需要再单独安装Jre）

三者的包含关系如图：

![](data:image/jpeg;base64,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)

## 2. Java类加载机制

### 2.1 类的生命周期

类的生命周期可分为：**加载、连接、初始化、使用和卸载**五个部分。

### 2.2 Java类加载流程

Java类加载主要是指生命周期中的**加载、连接、初始化**三个阶段。其中连接又可分为：**验证、准备、解析**三个部分。

+ 加载：这个阶段会在内存中生成一个代表这个类的 java.lang.Class 对象，作为方法区这个类的各种数据的入口，获取二进制字节流的方式可分为：

  + 从一个 Class 文件获取
  + 从 ZIP 包中读取，例如：jar 包和 war 包中读取
  + 运行时计算生成，例如：动态代理
  + 由其它文件生成，例如：将 JSP 文件转换成对应的 Class 类

+ 验证：确保 Class 文件的字节流中包含的信息符合当前虚拟机的要求，并且不会危害虚拟机自身的安全。

  可分为以下四个流程：

  + 文件格式验证
  + 元数据验证
  + 字节码验证
  + 符号引用验证

+ 准备：正式为类变量（被static修饰的变量）分配内存并设置类变量的初始值阶段，即在方法区中分配这些变量所使用的内存空间。实例变量不会在这阶段分配内存，它将会在对象实例化时随着对象一起分配在 Java 堆中。

+ 解析：虚拟机将常量池中的符号引用替换为直接引用的过程。

  + 符号引用：就是 class 文件中的CONSTANT_Class_info、CONSTANT_Field_info、CONSTANT_Method_info等变量，符号引用与虚拟机实现的布局无关，引用的目标并不一定要已经加载到内存中。各种虚拟机实现的内存布局可以各不相同，但是它们能接受的符号引用必须是一致的，因为符号引用的字面量形式明确定义在 Java 虚拟机规范的 Class 文件格式中。
  + 直接引用：指向目标的指针，相对偏移量或是一个能间接定位到目标的句柄。如果有了直接引用，那引用的目标必定已经在内存中存在

+ 初始化：初始化阶段才真正开始执行类中的定义的 Java 程序代码，虚拟机执行类构造器 <clinit>() 方法对类的静态变量赋予正确的初始值，JVM 负责对类进行初始化。

### 2.3 类加载器

+ **BootStrap ClassLoader**：启动类加载器，主要负责jdk_home/lib目录下的核心api或者x-bootclasspath 选项指定的jar包的装入工作。

+ **Extension ClassLoader**：扩展类加载器，主要负责jdk_home/lib/ext 目录下的jar包 或者 -Djava.ext.dirs指定目录下的jar包装入工作。
+ **System ClassLoader**：系统类加载器，主要负责 java -classpath / -Djava.class.path 所指目录下的类与jar。
+ **User Custom ClassLoader**：用户自定义加载器，通过java.lang.classloader的子类动态加载。

### 2.4 双亲委派模式

 双亲委派模式的工作流程：如果一个类加载器收到了类加载的请求，它首先不会自己去加载这个类，而是把请求委托给父加载器去完成，依次向上，因此，所有的类加载请求最终都应该被传递到顶层的启动类加载器中，只有当父加载器没有找到所需的类时，子加载器才会尝试去加载该类。

流程如图所示：

![](https://github.com/Newtol/interview/blob/master/Img/%E5%8F%8C%E4%BA%B2%E5%A7%94%E6%B4%BE.png)

双亲委派模式的好处：

+ 通过带有优先级的层级关可以避免类的重复加载，保证唯一性；
+ 保证 Java 程序安全稳定运行，Java 核心 API 定义类型不会被随意替换。

### 2.5 获取类的对象的三种方式

+ 类名.class，例如：String.class
+ 对象.getClass()，例如：”hello”.getClass()
+ Class.forName()，例如：Class.forName(“java.lang.String”)

## 3. JVM内存模型

JVM内存模型可分为：**线程共享**和**线程私有**两种。

+ 线程私有：线程私有数据区域生命周期与线程相同, 依赖用户线程的启动/结束而创建/销毁
  + **程序计数器**：是当前线程所执行的字节码的行号指示器，执行字节码工作时就是利用程序计数器来选取下一条需要执行的字节码指令,如果正在执行的是本地方法则为空,是唯一一个在虚拟机中没有规定任何 OutOfMemoryError 情况的区域。
  + **本地方法栈**：本地方法栈则为Native 方法服务
  + **虚拟机栈**：每个 Java 方法在执行的同时会创建一个栈帧用于存储局部变量表、操作数栈、常量池引用等信息。每一个方法从调用直至执行完成的过程，就对应着一个栈帧在 Java 虚拟机栈中入栈和出栈的过程。

+ 线程共享：线程共享区域随虚拟机的启动/关闭而创建/销毁。
  + **堆**（运行时内存）：创建的对象和数组都保存在 Java 堆内存中，也是垃圾收集器进行垃圾收集的最重要的内存区域。根据分代收集算法，堆又可以分为：新生代和老年代。
  + **方法区/永久代**：用于存储被 JVM 加载的类信息、常量、静态变量、即时编译器编译后的代码等数据。

### 3.1 JAVA堆

新生代：是用来存放新生的对象。一般占据堆的1/3空间。由于频繁创建对象，所以新生代会频繁触发MinorGC 进行垃圾回收。新生代又分为 **Eden 区**、**ServivorFrom**、**ServivorTo** 三个区。

+ 所有对象都创建在新生代的Eden区，当Eden区满后触发Minor GC,将Eden区和ServivorFrom去存活的对象复制到ServivorTo区中，并且将对象的“年龄”+1,如果达到进入老年代的条件（ServivorTo区空间不足或者年龄达到进入老年代条件），则将对象移动到老年代。
+ 保证一个Servivor区是空的，新生代Minor GC就是在两个Servivor区之间相互复制存活的对象，直到Servivor区满为止。

老年代：主要存放应用程序中生命周期长的内存对象，老年代的对象比较稳定，所以 MajorGC 不会频繁执行。

### 3.2 JAVA永久代

用于存放已被加载的类信息、常量、静态变量、即时编译器编译后的代码等数据。Class 在被加载的时候被
放入永久区域，它和和存放实例的区域不同**,GC 不会在主程序运行期对永久区域进行清理**。所以这
也导致了永久代的区域会随着加载的 Class 的增多而胀满，最终抛出 OOM 异常。

在Java8中，**永久代已经被移除，被一个称为“元数据区”（元空间）的区域所取代**。元空间
的本质和永久代类似，元空间与永久代之间最大的区别在于：元空间并不在虚拟机中，而是**使用**
**本地内存**。



## 4. 垃圾回收（GC）

### 4.1 GC机制概述

GC机制主要起到以下三个方面的作用：

+ 安全性考虑；
+ 减少内存泄露；
+ 减少程序员工作量

那些内存会被会被GC回收呢？

> 在Jvm内存模型中有介绍到Jvm内存被分为5个部分，其中程序计数器、虚拟机栈、本地方法栈由于是线程私有的，随线程而生，随线程而亡。因此这 3 个区域的内存分配和回收都是确定的，所以无需考虑内存回收的问题。但对于方法区和堆来说，是线程共享的，内存的分配和回收都是动态的，所以就需要考虑内存的回收问题，简而言之，**GC 主要进行回收的内存是 JVM 中的方法区和堆**。

是否具有GC机制后就不会有内存泄露了呢？

>  答案是否定的。因为对于一些无用但可达对象GC机制无法进行回收，这些对象的大量存在就会造成内存的泄露。例如：hibernate 的 Session（一级缓存）中的对象属于持久态，垃圾回收器是不会回收这些对象的，然而这些对象中可能存在无用的垃圾对象，如果不及时关闭（close）或清空（flush）一级缓存就可能导致内存泄露。

内存泄露和内存溢出有什么区别？

> 内存泄露：申请一块内存后，无法释放这块内存，丢失了这块内存的引用；
>
> 内存溢出：申请的内存不够，无法满足我们的需求

### 4.2 如何判断一个对象是否可回收

1. **引用计数法：**引用计数器算法是给每个对象设置一个计数器，当有地方引用这个对象的时候，计数器+1，当引用失效的时候，计数器-1，当计数器为 0 的时候，JVM 就认为对象不再被使用，就可以被回收。**引用计数器实现简单，效率高；但每次计数器的增加和减少都带来了很多额外的开销，且不能解决循环引用问题**（A 对象引用 B 对象，B 对象又引用 A 对象，但是A,B 对象已不被任何其他对象引用）。

2. **可达性分析（根搜索法）：** 根搜索算法是通过一些“GC Roots”对象作为起点，从这些节点开始往下搜索，搜索通过的路径成为引用链Reference Chain），当一个对象没有被 GC Roots 的引用链连接的时候，说明这个对象是不可用的。

   GC Roots 一般包含以下内容：

   > 1. 虚拟机栈中引用的对象
   > 2. 方法区中类静态属性引用的对象
   > 3. 方法区中的常量引用的对象
   > 4. 本地方法栈中引用的对象


### 4.3 JAVA 中引用类型

+ 强引用：在 Java 中最常见的就是强引用，把一个对象赋给一个引用变量，这个引用变量就是一个强引用。只要强引用还存在，GC 永远不会回收掉被引用的对象。因此**强引用是造成 Java 内存泄漏的主要原因之一**。

+ 软引用：软引用需要用 SoftReference 类来实现，对于只有软引用的对象来说，当系统内存足够时它不会被回收，当系统内存空间不足时它会被回收，即：**系统将会发生内存溢出了，才会对他们进行回收**。

+ 弱引用：弱引用需要用 WeakReference 类来实现，它比软引用的生存期更短，对于只有弱引用的对象来说，只要垃圾回收机制一运行，不管 JVM 的内存空间是否足够，总会回收该对象占用的内存，即：**只要进行 GC，就会对他们进行回收。**

+ 虚引用：虚引用需要 PhantomReference 类来实现，它**不能单独使用**，必须和引用队列联合使用。虚引用的主要作用是跟踪对象被垃圾回收的状态。


### 4.4 回收算法

+ **标记清除算法**（ Mark-Sweep ）：最基础的垃圾回收算法，分为两个阶段，**标注和清除**。标记阶段标记出所有需要回收的对象，清除阶段回收被标记的对象所占用的空间。标记—清除算法是基础的收集算法，缺点是**效率不高，而且清除后内存碎片化严重**
+ **复制算法**（Copying）：复制算法是把内存分成大小相等的两块，每次使用其中一块，当垃圾回收的时候，把存活的对象复制到另一块上，然后把这块内存整个清理掉。复制算法**实现简单，运行效率高，但是由于每次只能使用其中的一半，造成内存的利用率不高**。现在的 JVM 用复制方法收集新生代，由于新生代中大部分对象都是朝生夕死的，所以两块内存的比例不是 1:1(大概是 8:1)。
+ **标记—整理算法**（Mark-Compact）：标记-整理结合了上面两个算法，把存活对象往内存的一端移动，然后直接回收边界以外的内存。标记—整理算法**提高了内存的利用率，适合在收集对象存活时间较长的老年代。**
+  **分代收集算法**（Generational Collection）：分代收集是根据对象的存活时间把内存分为新生代和老年代，根据各个代对象的存活特点，每个代采用不同的垃圾回收算法。例如：**新生代采用复制算法，老年代采用标记—整理算法**

### 4.5 垃圾回收器



+ **Serial 垃圾收集器**（复制算法）：串行收集器，单线程处理垃圾回收工作，执行垃圾回收时所有线程都将暂停，**简单高效，没有线程交互的开销，是 java 虚拟机运行在 Client 模式下默认的新生代垃圾收集器。**

+ **ParNew 垃圾收集器**(复制算法）：ParNew收集器就是Serial收集器的多线程版本，是**很多java虚拟机运行在 Server 模式下新生代的默认垃圾收集器。**

+ **Parallel Scavenge 垃圾收集器**（复制算法）：并行收集器，在多个CPU下执行，适用于对吞吐量要求较高，多CPU，对系统响应时间无要求的系统应用。

+ **Serial Old 垃圾收集器**（标记-整理算法）：Serial Old 是 Serial 垃圾收集器年老代版本，这个收集器也主要是运行在 Client 默认的 java 虚拟机默认的年老代垃圾收集器。

+ **Parallel Old垃圾收集器**（标记-整理算法）：Parallel Old收集器是Parallel Scavenge的年老代版本。

+ **CMS 垃圾收集器**（标记-清除算法）：是一种年老代垃圾收集器，其最主要目标是获取最短垃圾回收停顿时间。整个垃圾回收过程分为以下 4 个阶段：

  > 初始标记：标记一下 GC Roots 能直接关联的对象，速度很快，仍然需要暂停所有的工作线程。
  >
  > 并发标记：进行 GC Roots 跟踪的过程，和用户线程一起工作，不需要暂停工作线程。
  >
  > 重新标记：为了修正在并发标记期间，因用户程序继续运行而导致标记产生变动的那一部分对象的标记记	   录，仍然需要暂停所有的工作线程。
  >
  > 并发清除：清除 GC Roots 不可达对象，和用户线程一起工作，不需要暂停工作线程。由于耗时最长的并发标记和并发清除过程中，垃圾收集线程可以和用户现在一起并发工作，所以总体上来看CMS 收集器的内存回收和用户线程是一起并发地执行。

+ **G1 垃圾收集器**（整体上采用标记-整理算法，局部采用复制算法） ：