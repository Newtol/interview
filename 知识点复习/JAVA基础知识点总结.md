## JAVA基础知识点总结

[TOC]


## 1. Java 基本数据类型

Java中总共有八种基本的数据类型：byte(1)、short(2)、int(4)、long(8)、char(2)、float(4)、double(8)和boolean【PS:括号内的为所占的字节数】,每种基本类型都有其对应的包装类。

### 1.1 自动类型转换

自动类型转换 ：低级变量可以直接转换为高级变量,转换规则为：

```
byte→short(char)→int→long→float→double
```

例如，下面的语句可以编译通过：

```java
byte b;
int i=b;
long l=b;
float f=b;
double d=b;
```

   但是将double型变量赋值给float变量，不加强转的话会报错。

### 1.2 自动装箱和自动拆箱

简单的说，装箱就是就是将基本数据类型转换为包装器类型；拆箱就是将包装器类型转换为基本数据类型。

例如：

```java
Integer i = 10;  //装箱
int n = i;   //拆箱
```

**注意事项**：

1. 对于Integer而言，如果数值在[-128,127]之间，便返回指向IntegerCache.cache中已经存在的对象的引用；否则创建一个新的Integer对象。例如：

   ```java
   public class Main {
       public static void main(String[] args) {         
           Integer i1 = 100;
           Integer i2 = 100;
           Integer i3 = 200;
           Integer i4 = 200;
           System.out.println(i1==i2);
           System.out.println(i3==i4);
       }
   }
   ```

   输出的结果就为：

   ```java
   true
   false
   ```

2. Integer i = new Integer(xxx)和Integer i =xxx;这两种方式的区别。

   + 第一种方式不会触发自动装箱的过程；而第二种方式会触发；
   + 在执行效率和资源占用上的区别。第二种方式的执行效率和资源占用在一般性情况下要优于第一种情况（注意这并不是绝对的）。

3. 当 **==**运算符的两个操作数都是包装器类型的引用，则是比较指向的是否是同一个对象，而如果其中有一个操作数是表达式（即包含算术运算）则比较的是数值（即会触发自动拆箱的过程）；另外，对于包装器类型，equals方法并不会进行类型转换。例如：

   ```java
   public class Main {
       public static void main(String[] args) {        
           Integer a = 1;
           Integer b = 2;
           Integer c = 3;
           Integer d = 3;
           Integer e = 320;
           Integer f = 320;
           Long g = 3L;
           Long h = 2L;
           // 因为c、d都是包装类型，所以返回true
           System.out.println(c==d);
           // 因为e、f都大于128，属于不同的对象，所以返回false
           System.out.println(e==f);
           // 因为含有算数运算符，所以比较的数值，返回true
           System.out.println(c==(a+b));
           // 因为equals不会类型转换，所以比较的是类型，返回true
           System.out.println(c.equals(a+b));
           // 比较数值，所以返回true
           System.out.println(g==(a+b));
           // 因为equals不会类型转换,a、b为Integer，所以返回false
           System.out.println(g.equals(a+b));
           // a向上转型为Long,所以返回true
           System.out.println(g.equals(a+h));
       }
   }
   ```

### 1.3 int 和 和 Integer 有什么区别？

1. Integer是int的包装类；int是基本数据类型； 
2. Integer变量必须实例化后才能使用；int变量不需要； 
3. Integer实际是对象的引用，指向此new的Integer对象；int是直接存储数据值 ； 
4. Integer的默认值是null；int的默认值是0。

### 1.4 String、StringBuffer、StringBuilder的区别：

1. 是否可变：
   + String：字符串常量，在修改时不会改变自身；若修改，等于重新生成新的字符串对象。
   + StringBuffer、StringBuilder：在修改时会改变对象自身，每次操作都是对 StringBuffer 对象本身进行修改，不是生成新的对象；使用场景：对字符串经常改变情况下，主要方法：append（），insert（）等。
2. 是否线程安全：
   + String：对象定义后不可变，线程安全。
   + StringBuilder：是线程不安全的，适用于单线程下操作字符串缓冲区大量数据。
   + StringBuffer：是线程安全的（对调用方法加入同步锁），执行效率较慢，适用于多线程下操作字符串缓冲区大量数据。
3. String不可变有什么好处？
   + 可以缓存 hash 值
   + String Pool 的需要
   + 线程安全

## 2. Java 修饰符

Java修饰符：用来定义类、方法或者变量，通常放在语句的最前端。可分为：

- 访问修饰符
- 非访问修饰符

### 2.1 访问修饰符

 Java中具有四种访问权限：

- **public** : 对所有类可见。使用对象：类、接口、变量、方法
- **protected** : 对同一包内的类和所有子类可见。使用对象：变量、方法。 **注意：不能修饰类（外部类）**。

- **default** (即缺省，什么也不写）: 在同一包内可见，不使用任何修饰符。使用对象：类、接口、变量、方法。
- **private** : 在同一类内可见。使用对象：变量、方法。 **注意：不能修饰类（外部类）**

访问权限之间的对比如下表所示：

![](https://github.com/Newtol/interview/blob/master/Img/Java%E8%AE%BF%E9%97%AE%E4%BF%AE%E9%A5%B0%E7%AC%A6.png)

### 2.2 非访问修饰符

Java中提供的非访问修饰符有：

- static：用来**修饰类、方法和变量**。
  - static修饰变量：类所有的实例都共享静态变量，可以直接通过类名来访问它；
  - static修饰方法：静态方法在类加载的时候就存在了，它不依赖于任何实例，所以 static 方法必须实现，也就是说它不能是抽象方法（abstract）。
  - static修饰语句块：静态语句块在类初始化时运行一次。
  - static修饰内部类：静态内部类不依赖外部类，且不能访问外部类的非 static 变量和方法。

- final：用来**修饰类、方法和变量**:
  - final 修饰类：不能够被继承
  - final 修饰方法：不能被继承类重新定义；
  - final 修饰变量：如果为基本类型，则数值不可改变，为常量；若为引用类型，则引用不能更改，但引用的对象本身的属性可更改。

- abstract：用来**创建抽象类和抽象方法**。

- synchronized 和 volatile：主要用于线程的编程。

注意事项：

1. 静态成员函数中**不能**调用非静态成员；
2. 非静态成员函数**可以**调用静态成元；
3. 常量成员不能修改，静态成员必须初始化，但可以修改；
4. 静态成员和静态方法可以直接通过类名进行调用，其他成员方法则需要进行实例化后调用。

### 2.3 Java变量

Java中的变量可分为三种类型：

- 成员变量
- 局部变量
- 静态变量

它们三者的区别如下图所示：

![](https://github.com/Newtol/interview/blob/master/Img/%E6%88%90%E5%91%98%E5%8F%98%E9%87%8F_%E9%9D%99%E6%80%81%E5%8F%98%E9%87%8F_%E5%B1%80%E9%83%A8%E5%8F%98%E9%87%8F.png)

## 3. Java 继承

Java面对对象具有三大特性：

1. 继承：继承是从已有类得到继承信息创建新类的过程。提供继承信息的类被称为父类（超类、基类）；得到继承信息的类被称为子类（派生类）。继承让变化中的软件系统有了一定的延续性，同时继承也是封装程序中可变因素的
2. 封装：通常认为封装是把数据和操作数据的方法绑定起来，对数据的访问只能通过已定义的接口
3. 多态：多态是指允许不同子类型的对象对同一消息作出不同的响应。要实现多态主要是做两件事：重写和重载。

### 3.1 方法重载和方法重写

重载：是在一个类里面，是多态在编译器的表现形式。判断方法：

- 方法名相同
- 形参列表不同

重写：是子类对父类的允许访问的方法的实现过程进行重新编写, 返回值和形参都不能改变。是多态的运行期间的表现形式。判断条件：

- 方法名和形参列表相同
- 重写方法的返回值或者抛出的异常类型要与被重写的方法的返回值和抛出的异常相同，或者为其子类
- 重写方法的访问修饰符大于等于被重写方法的访问修饰符

注意事项：

- 静态方法不存在重写，形式上的重写只能说是隐藏；
- 私有方法不存在重写，父类中的private方法，子类中即使定义了也相当于一个新的方法；

### 3.2 抽象类和接口

抽象类（abstract）和接口（interface）的区别：

1. 抽象类中可以有构造方法，接口中不能；
2. 抽象类中可以有普通成员变量，接口中不能；
3. 抽象类中可以包含非抽象的普通方法，接口不能；
4. 抽象类中的访问类型是：public、protected，接口中默认为：public abstract;
5. 抽象类中可以包含静态方法，接口中不能；
6. 抽象类中的静态成员变量类型任意，接口中仅为：public static final;
7. 一个类只可以继承（extends）一个抽象类，但一个类可以继承（implements）多个接口；

### 3.3 super和this关键字

this关键字：是指向对象本身的一个指针。this只能在类中的非静态方法中使用，静态方法和静态的代码块中绝对不能出现this。

+ 表示类中的属性和方法：函数参数或者参数中的局部变量和成员变量同名的情况下，成员变量被屏蔽，此时要访问成员变量则需要用"this.成员变量名"来访问成员变量。例如:

  ```java
  class B{
      private int x = 1;
      public void out(){
          int x = 2;
          System.out.print(x);//打印2
          System.out.print(this.x);//打印1
      }
  }
  ```

+ 表示当前对象：在函数中，需要引用该函数所属类的当前对象时候，直接使用this

  ```java
  class C{
      public static void main(String[] args){
          C c1 = new C();
          c1.tell();
      }
      public static void tell(){
          System.out.print(this);//打印当前对象的字符串表示
      }
  }
  ```

super关键字：

+ 子类调用父类的构造方法：用`super(参数列表)`的方式调用，参数不是必须的。同时，还要注意`super(参数列表)`这条语句只能在子类构造方法中的第一行。例如：	

  ```java
  class A{
      public A(){
          System.out.print("A");
      }
  }
  class B extends A{
      public B(){
          super();//调用父类构造方法，打印A
          System.out.print("B");
      }
  }
  ```

+ 访问父类中被覆盖的同名变量或者方法：如果子类覆盖了父类的中某个方法的实现，可以通过使用 super 关键字来引用父类的方法实现。例如：

  ```java
  class A{
      public int a = 1;//可以直接赋值，不用通过构造函数
      public void say(){
          System.out.print(a);
      }
  }
  
  class B extends A{
      private int a = 2;
      public void say(){
          System.out.print(super.a);//访问父类的a变量，前提是父类的a变量是公有的
      }
      public void tell(){
          super.say();//调用父类的say()方法而不是子类的say()方法
      }
  }
  ```

### 3.4 Java构造器

在Java中，构造方法的主要作用是完后才能对象的初始化工作，把定义对象的参数传给对象的域。

注意事项：

1. 构造方法的方法名必须与类名相同；

2. 构造方法没有返回类型，也不能定义为void，在方法名前不声明方法类型；

3. 一个类可以定义多个构造方法，如果类在定义时没有定义构造方法，编译器会自动插入一个无参数的默认构造器；

4. 子类**不继承**父类的构造器（构造方法或者构造函数）的，它只是**调用**（隐式或显式）。如果父类的构造器带有参数，则必须在子类的构造器中显式地通过 super 关键字调用父类的构造器并配以适当的参数列表。如果父类构造器没有参数，则在子类的构造器中不需要使用 super 关键字调用父类构造器，系统会自动调用父类的无参构造器。


## 4. Java 异常

Java把异常当作对象来处理，并定义一个基类`java.lang.Throwable`作为所有异常的超类。

### 4.1 Java异常分类

throwable又可以分为两类：

+ Error：内部错误或者资源耗尽错误，当出现这些异常时，Java虚拟机（JVM）一般会选择终止线程
+ Exception：通常情况下是可以被程序处理的，并且在程序中应该尽可能的去处理这些异常。

Exception又可分为：

+ UncheckedException：是程序运行时错误，常见的异常有：
  + ClassNotFoundException：应用程序试图加载类时，找不到相应的类，抛出该异常。
  + IllegalAccessException：拒绝访问一个类的时候，抛出该异常。
  + InterruptedException：一个线程被另一个线程中断，抛出该异常。
  + NoSuchMethodException：请求的方法不存在
  + NullPointerException：空指针异常
  + IndexOutOfBoundsException： 数组角标越界异常，常见于操作数组对象时发生。
  + ClassCastException： 数据类型转换异常
  + NumberFormatException： 字符串转换为数字异常；出现原因：字符型数据中包含非数字型字符。
+ CheckedException：需要用 try...catch... 语句捕获并进行处理，并且可以从异常中恢复，常见的有：
  + IOException
  + SQLException

### 4.2 异常处理机制

Java的异常处理机制可分为：

+ 异常捕获：**try、catch 和 finally**
+ 异常抛出：**throws、throw**

对于异常捕获，我们需要注意的是一下几点：

try语句在返回前，将其他所有的操作执行完，保留好要返回的值，而后转入执行finally中的语句，而后分为以下三种情况：

+ 情况一：如果finally中有return语句，则会将try中的return语句”覆盖“掉，直接执行finally中的return语句，得到返回值，这样便无法得到try之前保留好的返回值。

+ 情况二：如果finally中没有return语句，也没有改变要返回值，则执行完finally中的语句后，会接着执行try中的return语句，返回之前保留的值。

+ 情况三：如果finally中没有return语句，但是改变了要返回的值，这里有点类似与引用传递和值传递的区别，分以下两种情况：

  + 如果return的数据是基本数据类型或文本字符串，则在finally中对该基本数据的改变不起作用，try中的return语句依然会返回进入finally块之前保留的值。

  + 如果return的数据是引用数据类型，而在finally中对该引用数据类型的属性值的改变起作用，try中的return语句返回的就是在finally中改变后的该属性的值

对于异常的抛出，需要注意的是：throws和throw的区别，

throw：

+ throw 语句用在方法体内，表示抛出异常，由方法体内的语句处理。
+ throw 是具体向外抛出异常的动作，所以它抛出的是一个异常实例，执行 throw 一定是抛出了某种异常

throws：

+ throws 语句是用在方法声明后面，表示如果抛出异常，由该方法的调用者来进行异常的处理。
+ throws 主要是声明这个方法会抛出某种类型的异常，让它的使用者要知道需要捕获的异常的类型。
+ throws 表示出现异常的一种可能性，并不一定会发生这种异常。

## 5. Java Object

### 5.1 Object方法概述

Java中的Object类是所有类的父类，它提供了以下11个方法：

1. `public final native Class<?> getClass()`：返回当前运行时对象的Class对象，getClass方法是一个final方法，不允许子类重写，并且也是一个native方法。

2. `public native int hashCode()`： 返回散列值，而 equals() 是用来判断两个实例是否等价。等价的两个实例散列值一定要相同，但是散列值相同的两个实例不一定等价。

3. `public boolean equals(Object obj)`：在非空对象引用上equlas具有以下特性：

   （一）自反性

   ```
   x.equals(x); // true
   ```

   （二）对称性

   ```
   x.equals(y) == y.equals(x) // true
   ```

   （三）传递性

   ```
   if(x.equals(y) && y.equals(z)) {
       x.equals(z); // true;
   }
   ```

   （四）一致性：多次调用 equals() 方法结果不变

   ```
   x.equals(y) == x.equals(y); // true
   ```

   （五）与 null 的比较：对任何不是 null 的对象 x 调用 x.equals(null) 结果都为 false

   ```
   x.euqals(null); // false;
   ```

4. `protected native Object clone() throws CloneNotSupportedException`：是一个protected的native方法。由于Object本身没有实现Cloneable接口，所以不重写clone方法并且进行调用的话会抛出异常。且clone函数具有以下特性：

   + x.clone()!=x：x.clone()返回的对象为新建的对象，与原来的对象地址不同。
   + x.clone().getClass() == x.getClass(）：克隆出的对象与原对象都是同一个类生成的。   
   + x.clone().equals(x)：新的对象与原来的对象相同（在equals()函数下是相同的,所以通常需要覆盖equals()方法） 

5. `public String toString()`：Object对象的默认实现，即输出类的名字@实例的哈希码的16进制

6. `public final native void notify()`：是一个native方法，并且也是final的，不允许子类重写。唤醒一个在此对象监视器上等待的线程(监视器相当于就是锁的概念)。如果所有的线程都在此对象上等待，那么只会选择一个线程。选择是任意性的，并在对实现做出决定时发生。

7. `public final native void notifyAll()`：跟notify一样，唯一的区别就是会唤醒在此对象监视器上等待的所有线程，而不是一个线程。

8. `public final native void wait(long timeout) throws InterruptedException`：是一个native方法，并且也是final的，不允许子类重写。wait方法会让当前线程等待直到另外一个线程调用对象的notify或notifyAll方法，或者超过参数设置的timeout超时时间。

9. `public final void wait(long timeout, int nanos) throws InterruptedException`：跟wait(long timeout)方法类似，多了一个nanos参数，这个参数表示额外时间（以毫微秒为单位，范围是 0-999999）

10. `public final void wait() throws InterruptedException`：跟之前的2个wait方法一样，只不过该方法一直等待，没有超时时间。

11. `protected void finalize() throws Throwable { }`：该方法的作用是实例被垃圾回收器回收的时候触发的操作finalize方法是一个protected方法，Object类的默认实现是不进行任何操作。

### 5.2 “==”和equals的区别：

> `==`：如果比较的对象是基本数据类型，则比较的是数值是否相等；如果比较的是引用数据类型，则比较的是对象的地址值是否相等。在不遇到算术运算的情况下，不会自动拆箱。
> `equals()`：用来比较方法两个对象的内容是否相等。
> 注意：equals 方法不能用于基本数据类型的变量，如果没有对 equals 方法进行重写，则比较的是引用类型的变量所指向的对象的地址。

### 5.3为什么重写equals方法后需要重写hashcode?

> 因为考虑到类似HashMap、HashTable、HashSet的这种散列的数据类型的运用。在Object类中，hashCode方法是通过Object对象的地址计算出来的，因为Object对象只与自身相等，所以同一个对象的地址总是相等的，计算取得的哈希码也必然相等，对于不同的对象，由于地址不同，所获取的哈希码自然也不会相等。所以如果重写了equals方法，而不重写hashcode方法，就可能会造成两个相同对象的重复插入。

### 5.4 notify()和notifyAll有什么区别？

> notify()方法不能唤醒某个具体的线程，所以只有一个线程等待的时候才有用。而notifyAll（）唤醒所有的线程，并允许他们争夺锁，确保只有一个线程能继续运行

### 5.5 为什么wait/notify/notifyAll是Object而不是Thread方法？

>Java提供的锁是对象级的而不是线程级。每个对象都有锁，通过线程获得。因为它们属于锁的操作，而锁属于对象。

### 5.6 clone一个对象和new 一个对象的区别

>new一个对象： 先根据*new*后面的类型去分配内存，然后再调用构造函数填充对象的各个域，初始化完成后，一个对象创建完毕，可以把他的引用（地址）发布到外部。
>
>clone一个对象：首先分配与原对象同样大小的内存空间，然后根据原对象中对应的各个域，填充新对象的域，填充完成之后，clone 方法返回，一个新的相同的对象被创建，同样可以把这个新对象的引用发布到外部

### 5.7 深拷贝和浅拷贝

> 浅拷贝：拷贝实例和原始实例的引用类型引用同一个对象；
>
> 深拷贝：拷贝实例和原始实例的引用类型引用不同对象。

原理图大概如图所示：

![](https://github.com/Newtol/interview/blob/master/Img/%E6%B7%B1%E6%8B%B7%E8%B4%9D_%E6%B5%85%E6%8B%B7%E8%B4%9D.png)

## 6. Java反射

Java 中的反射首先是能够获取到Java中要反射类的字节码 ，获取字节码有三种方法 ：

+ Class.forName(className) 
+ 类名.class 
+ this.getClass()

然后将字节码中的方法，变量，构造函数等映射成相应的 Method、Filed、Constructor 等类，这些类提供了丰富的方法可以被我们所使用。

### 6.1 反射的作用

Java反射机制主要提供一下的功能：

1. 在运行时判断任意一个对象所属的类
2. 在运行时构造任意一个类的对象
3. 在运行时判断任意一个类所具有的成员变量和方法
4. 在运行时调用任意一个对象的方法
5. 生成动态代理

### 6.2 静态代理和动态代理

静态代理：通常只代理一个类，事先知道要代理的是什么。

动态代理：动态代理是代理一个接口下的多个实现类，不知道要代理什么东西，只有在运行时才知道。动态代理是实现 JDK 里的 InvocationHandler 接口的 invoke 方法，但注意的是代理的是接口，也就是你的业务类必须要实现接口，通过 Proxy 里的 newProxyInstance 得到代理对象。

例如：下图为实现一个ArrayList的动态代理类：

```java
public class proxy {
    public static void main(String[] args) {
        final ArrayList<String> list = new ArrayList<>();
        ClassLoader classLoader = list.getClass().getClassLoader();
        Class<?>[] interfaces = list.getClass().getInterfaces();
        List<String> listProxy=(List<String>) Proxy.newProxyInstance(classLoader,interfaces , new InvocationHandler() {
            @Override
            public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
                return method.invoke(list,args);
            }
        });
        listProxy.add("你好") ;
        System.out.println(list);
    }
}
```

还有一种动态代理 CGLIB，代理的是类，不需要业务类继承接口，通过派生的子类来实现代理。通过在运行
时，动态修改字节码达到修改类的目的。

## 7. Java 注解

Java 注解是附加在代码中的一些元信息，用于一些工具在编译、运行时进行解析和使用，起到说明、配置的功能。

其中Java有四种元注解，用来标注其他的注解：

+ @Target: 修饰的对象范围。
+ @Retention： 定义被保留的时间长短
  + SOURCE:在源文件中有效（即源文件保留）
  + CLASS:在 class 文件中有效（即 class 保留）
  + RUNTIME:在运行时有效（即运行时保留）
+ @Documented：  描述-javadoc
+ @Inherited ：  阐述了某个被标注的类型是被继承的

## 8. Java 泛型





