

# 面向对象：封装

封装的步骤：防止数据被随意篡改

## 1.使用 `private` 关键字来修饰成员变量。

## 2.使用`public`修饰getter和setter方法。

例子：

```java
public class Student {
    private String name;
    private int age;
//使用 `private` 关键字来修饰成员变量。
    public void setName(String n) {
      	name = n;
    }

    public String getName() {
      	return name;
    }

    public void setAge(int a) {
        if (a > 0 && a <200) {
            age = a;
        } else {
            System.out.println("年龄非法！");
        }
    }

    public int getAge() {
      	return age;
        //使用`public`修饰getter和setter方法。
    }
}
```



# 面向对象：继承

假如多个类中存在相同属性和行为时，我们可以将这些内容抽取到单独一个类中，那么多个类无需再定义这些属性和行为，只要**继承**那一个类即可。其中，多个类可以称为**子类**，单独被继承的那一个类称为**父类**、**超类（superclass）**或者**基类**。



## 继承的含义

继承描述的是事物之间的所属关系，这种关系是：`is-a` 的关系。例如，兔子属于食草动物，食草动物属于动物。可见，**<u>父类更通用，子类更具体</u>**。我们通过继承，可以使多种事物之间形成一种关系体系。

**继承**：就是子类继承父类的**属性**和**行为**，使得子类对象可以直接具有与父类相同的属性、相同的行为。子类可以<u>直接访问父类中的**非私有**的属性和行为。</u>

## 继承的好处

1. 提高**代码的复用性**（减少代码冗余，相同代码重复利用）。
2. 使类与类之间产生了关系。

## 继承的格式

通过 `extends` 关键字，可以声明一个子类继承另外一个父类。

**注意：Java是单继承的，一个类只能继承一个直接父类，跟现实世界很像，但是Java中的子类是更加强大的。**





<img src="https://gitee.com/qhzeng/markdown/raw/master/image/360%E6%88%AA%E5%9B%BE20181202211331250.jpg" alt="360截图20181202211331250" style="zoom:67%;" />



## 子类不能继承的内容

并不是父类的所有内容都可以给子类继承的：

**1.子类不能继承父类的构造器，因为子类有自己的构造器。**

**子类<u>可以继承父类的私有成员（成员变量，方法），只是子类无法直接访问而已</u>，可以通过getter/setter方法访问父类的private成员变量。**



## 继承后的特点—成员变量

### 成员变量不重名

如果子类父类中出现**不重名**的成员变量，这时的访问是**没有影响的**。

### 成员变量重名

如果子类父类中出现**重名**的成员变量，这时的访问是**有影响的**。

**子父类中出现了同名的成员变量时，子类会优先访问自己对象中的成员变量。如果此时想访问父类成员变量，可以使用super关键字**

### super访问父类成员变量

子父类中出现了同名的成员变量时，在子类中需要访问父类中非私有成员变量时，需要使用`super` 关键字，修饰父类成员变量，类似于之前学过的 `this` 。

需要注意的是：**super代表的是父类对象的引用，this代表的是当前对象的引用。**

**使用格式：**

```java
super.父类成员变量名
```



## 继承后的特点—成员方法

### 成员方法不重名

如果子类父类中出现**不重名**的成员方法，这时的调用是**没有影响的**。对象调用方法时，会**先在子类中查找有没有对应的方法**，若子类中存在就会执行子类中的方法，若子类中不存在就会执行父类中相应的方法。





### 成员方法重名

如果子类父类中出现**重名**的成员方法，则创建子类对象调用该方法的时候，子类对象会优先调用自己的方法。



## 方法重写

**方法重写** ：**<u>子类中出现与父类一模一样的方法</u>**时（返回值类型，方法名和参数列表都相同），会出现覆盖效果，也称为重写或者复写。**声明不变，重新实现**。

### 使用场景与案例

发生在子父类之间的关系。
子类继承了父类的方法，但是子类觉得父类的这方法不足以满足自己的需求，子类重新写了一个与父类同名的方法，以便覆盖父类的该方 法。

**@Override重写注解校验！**



### 注意事项 

1. 方法重写是发生在子父类之间的关系。
2. 子类方法覆盖父类方法，必须要保证**权限大于等于父类权限**。
3. 子类方法覆盖父类方法，返回值类型、函数名和参数列表都要一模一样。
4. 与【方法重载overload】区分发生在构造方法中，方法名字相同，参数列表不同。





## 继承后的特点—构造器

首先我们要回忆两个事情，构造器的定义格式和作用。

1. 构造器的名字是与类名一致的。所以子类是无法继承父类构造方法的。
2. 构造器的作用是初始化对象成员变量数据的。所以子类的初始化过程中，必须先执行父类的初始化动作。子类的构造方法中默认有一个`super()` ，表示调用父类的构造方法，父类成员变量初始化后，才可以给子类使用。（**先有爸爸，才能有儿子**）

**继承后子类构造器特点:子类所有构造器的第一行都会先调用父类的无参构造器，再执行自己**

```java
class Person {
    private String name;
    private int age;

    public Person() {
        System.out.println("父类的无参构造方法");
    }
    // getter/setter省略
}

class Student extends Person {
    private double score;

    public Student() {
        super(); // 调用父类无参,默认就存在，可以不写，必须再第一行
        System.out.println("子类无参构造方法");
    }
    
     public Student(double score) {
        //super();  // 调用父类无参,默认就存在，可以不写，必须再第一行
        this.score = score;    
        System.out.println("子类有参");
     }

}

public class Demo07 {
    public static void main(String[] args) {
        Student s1 = new Student();
        System.out.println("----------");
        Student s2 = new Student(99.9);
    }
}

```

* 子类构造器执行的时候，都会在第一行默认先调用父类无参数构造器一次。
* 子类构造器的第一行都隐含了一个**super()**去调用父类无参数构造器，**super()**可以省略不写。
* super只能有一个，并且不许放在第一行，默认调用无参构造方法，可以调用其他构造方法



## this关键字



### this关键字的作用

this代表**<u>所在类</u>**的**<u>当前对象</u>**的引用（地址值），即代表当前对象。

### this关键字的应用

在getter setter方法中：



在构造器中
```java
public class Student {
    private String name;
    private int age;
    
// 无参数构造方法
    public Student() {} 

    // 有参数构造方法
    public Student(String name,int age) {
        this.name = name;
        this.age = age; 
    }
}
```





super(...) -- 调用父类的构造器，根据参数匹配确认
this(...) -- 调用本类的其他构造器，根据参数匹配确认







## super与this区分



super关键字用来访问父类的内容，this关键字用来访问本类的内容

### super

1.在子类的成员方法中，调用父类成员变量

`super.num;`

2.在子类的成员方法中，调用父类成员方法

`super.show();`

3.在子类的构造方法中，调用父类构造方法

```java
class Student extends Person {
    private double score = 100;

    public Student() {
        //super(); // 调用父类无参构造器,默认就存在，可以不写，必须再第一行
        System.out.println("子类无参");
    }
    
     public Student(String name ， int age，double score) {
        super(name ,age);// 调用父类有参构造器Person(String name , int age)初始化name和age
        this.score = score;    
        System.out.println("子类有参");
     }
      // getter/setter省略
}

```



### this

1.在本类的成员方法中，访问本类的成员变量

`this.num;`

2.在本类的成员方法中，访问本类的另一个成员方法

`this.hello();`

3.在本类的构造方法中，调用本类的另一个构造方法（构造方法的本类调用。必须是构造方法的第一个语句）

```java
class Student{
    private String name ;
    private int age ;
    private char sex ;

    public Student() {
  // 很弱，我的兄弟很牛逼啊，我可以调用其他构造器：Student(String name, int age, char sex)
        this("徐干",21,'男');
    }

    public Student(String name, int age, char sex) {
        this.name = name ;
        this.age = age   ;
        this.sex = sex   ;
    }
```



### 小结

![image-20210425155651507](https://gitee.com/qhzeng/markdown/raw/master/image/image-20210425155651507.png)

* **子类的每个构造方法中均有默认的super()，调用父类的空参构造。手动调用父类构造会覆盖默认的super()。**
* **super() 和 this() 都必须是在构造方法的第一行，所以不能同时出现。**
* **super(..)和this(...)是根据参数去确定调用父类哪个构造器的。**
* super(..)可以调用父类构造器初始化继承自父类的成员变量的数据。
* this(..)可以调用本类中的其他构造器。



# 抽象类和抽象方法

## 抽象类和抽象方法

父类中的方法，被它的子类们重写，子类各自的实现都不尽相同。那么父类的方法声明和方法主体，只有声明还有意义，而方法主体则没有存在的意义了(因为子类对象会调用自己重写的方法)。换句话说，父类可能知道子类应该有哪个功能，但是功能具体怎么实现父类是不清楚的（由子类自己决定），父类完全只需要提供一个没有方法体的方法签名即可，具体实现交给子类自己去实现。**我们把没有方法体的方法称为抽象方法。**

**Java语法规定，包含抽象方法的类就是抽象类**。



- **抽象方法** ： 没有方法体的方法。
- **抽象类**：包含抽象方法的类。

### 抽象方法

使用`abstract` 关键字修饰方法，该方法就成了抽象方法，抽象方法**只包含一个方法名，而没有方法体。**

定义格式：

```java
修饰符 abstract 返回值类型 方法名 (参数列表)；
```

```java
public abstract void run()；
```

### 抽象类

如果一个类包含抽象方法，那么该类必须是抽象类。

**注意：抽象类不一定有抽象方法，但是有抽象方法的类必须定义成抽象类。**

定义格式：

```java
abstract class 类名字 { 
}

```

```java
public abstract class Animal {
    public abstract void run()；
}
```

### 抽象类的使用

**要求**：继承抽象类的子类**必须重写父类所有的抽象方法**。否则，该子类也必须声明为抽象类。

## 抽象类的特征

抽象类的特征总结起来可以说是 **有得有失**

**有得：抽象类得到了拥有抽象方法的能力。**

**有失：抽象类失去了创建对象的能力。**

其他成员（构造器，实例方法，静态方法等）抽象类都是具备的。

## 抽象类的注意事项

关于抽象类的使用，以下为语法上要注意的细节，虽然条目较多，但若理解了抽象的本质，无需死记硬背。

1. 抽象类**不能创建对象**，如果创建，编译无法通过而报错。只能创建其非抽象子类的对象。

   > 理解：假设创建了抽象类的对象，调用抽象的方法，而抽象方法没有具体的方法体，没有意义。

2. 抽象类中，可以有构造器，是供子类创建对象时，初始化父类成员使用的。

   > 理解：子类的构造方法中，有默认的super()，需要访问父类构造方法。

3. 抽象类中，不一定包含抽象方法，但是有抽象方法的类必定是抽象类。

   > 理解：未包含抽象方法的抽象类，目的就是不想让调用者创建该类对象，通常用于某些特殊的类结构设计。

4. 抽象类的子类，必须重写抽象父类中**所有的**抽象方法，否则子类也必须定义成抽象类，编译无法通过而报错。 

   > 理解：假设不重写所有抽象方法，则类中可能包含抽象方法。那么创建对象后，调用抽象的方法，没有意义。

5. 抽象类存在的意义是为了被子类继承，抽象类体现的是模板思想。

   > 理解：抽象类中已经实现的是模板中确定的成员，抽象类不确定如何实现的定义成抽象方法，交给具体的子类去实现。





# 接口

接口是更加彻底的抽象，接口中全部是抽象方法。**将抽象进行到底！！** 

接口的字节码文件同样是`.class`

## 接口包含的内容JDK

Java7

### 		1.常量

### 		2.抽象方法

Java8

### 		3.默认方法

### 		4.静态方法

Java9

### 		5.私有方法



## 定义格式

```java
//接口的定义格式：
修饰符 interface 接口名称{
    // 抽象方法
}

// 修饰符：public|缺省
// 接口的声明：interface
// 接口名称：首字母大写，满足“驼峰模式”
```

## 接口成分特点

  在JDK8之前，接口中的成分包含：抽象方法和常量

### 1.抽象方法

注意：

接口中的抽象方法默认会自动加上`public abstract`修饰程序员无需自己手写！！
​       

按照规范：以后接口中的抽象方法可以不用写上public abstract。默认会有

```java
   public abstract void methodAbs1();

    abstract void methodAbs2();

    void methodAbs3();

    public void methodAbs4();
//这些都是抽象方法
```



### 2.常量

 在接口中定义的成员变量默认会加上： public static final修饰。也就是说在接口中定义的成员变量实际上是一个常量。这里是使用public static final修饰后，变量值就不可被修改，并且是静态化的变量可以直接用接口名访问，所以也叫常量。常量必须要给初始值。常量命名规范建议字母全部大写，多个单词用下划线连接。

## 实现接口

接口不能直接使用，必须有一个实现类。

类与接口的关系为实现关系，即**类实现接口**，该类可以称为接口的实现类，也可以称为接口的子类。实现的动作类似继承，格式相仿，只是关键字不同，实现使用 ` implements`关键字。

```java
/**接口的实现：
    在Java中接口是被实现的，实现接口的类称为实现类。
    实现类的格式:*/
[修饰符] class 类名 implements 接口1,接口2,接口3...{
}
```



## 类实现接口的要求和意义

1. **<u>必须重写实现的全部接口中所有抽象方法。</u>**
2. **如果一个类实现了接口，但是没有重写完全部接口的全部抽象方法，这个类也必须定义成抽象类。**
3. **意义：接口体现的是一种规范，接口对实现类是一种强制性的约束，要么全部完成接口申明的功能，要么自己也定义成抽象类。这正是一种强制性的规范。**



## JDK 8之后的接口新增方法

从JDK 8开始之后，接口不再纯洁了，接口中不再只是抽象方法，接口还可以有**默认方法**（也就是实例方法），和**静态方法**了，还包含了私有实例方法和私有静态方法



## 1 含有默认方法和静态方法

**默认方法：使用 `default` 修饰，不可省略，供子类调用或者子类重写。**

​			默认方法可以通过接口**实现类对象直接调用**，也可以通过接口实现类**覆盖重写**

**静态方法：使用 `static` 修饰，供接口直接调用。**

​				`接口名称.静态方法`   不能通过实现类的对象来调用



代码如下：

```java
public interface InterFaceName {
    public default void method() {
        // 执行语句
    }
    public static void method2() {
        // 执行语句    
    }
}
```



## 2 含有私有方法和私有静态方法（JAVA9开始）

我们想要抽取一个公有方法，用来解决两个默认方法时间的代码重复问题，但是这个公有方法不想被实现类使用，应该是私有化的



**普通私有方法：使用 `private` 修饰，供接口中的默认方法或者静态方法调用。**

代码如下：

```java
public interface InterFaceName {
    private void method() {
        // 执行语句
    }
}
```

**静态私有方法：解决多个静态方法时间代码重复问题**

```java
public interface InterFaceName {
    private static void method() {
        // 执行语句
    }
}
```



### 新增方法的使用

**默认方法和静态方法以及私有方法和私有静态方法**，**遵循面向对象的继承关系使用原则，实现类依然可以访问接口的非私有方法，对于接口中的非私有静态方法，可以直接通过接口名进行访问。**

重写默认方法注意（了解）:

* 子接口重写默认方法时，default关键字可以保留。

* 实现类重写默认方法时，default关键字不可以保留。





## 接口小结

- 接口中，无法定义成员变量，但是可以定义常量，其值不可以改变，默认使用public static final修饰。
- 接口中的方法全是抽象方法，默认会自动加上public abstract修饰
- JDK 8开始，接口不再纯洁，支持静态方法，默认方法，**JDK9:私有方法。**
- 接口中，没有构造器，**不能创建对象**。
- 类与接口是多实现的
- 接口与接口是多继承的
- 接口体现的规范。

<img src="https://gitee.com/qhzeng/markdown/raw/master/image/image-20210426155653336.png" alt="image-20210426155653336" style="zoom: 50%;" />



<img src="https://gitee.com/qhzeng/markdown/raw/master/image/image-20210426160439327.png" alt="sss" style="zoom:67%;" />





## 接口与接口的多继承

Java中，接口与接口之间是可以多继承的：也就是一个接口可以同时继承多个接口。大家一定要注意：

**类与接口是实现关系**

**接口与接口是继承关系**

接口继承接口就是把其他接口的抽象方法与本接口进行了合并。

**类与类之间是单继承的，直接父类只有一个**

**类与接口之间是多实现的，一个类可以实现多个接口**

**接口与接口之间是多继承的**

注意事项：

1.多个父接口中的抽象方法如果重复，没关系，只需要集成其中一个

2.多个父接口当中的默认default方法如果重复，那么子接口必须进行默认方法的覆盖重写。

## 实现多个接口使用注意事项

### 多个接口同名静态方法

如果实现了多个接口，多个接口中存在同名的静态方法并不会冲突，原因是只能通过各自接口名访问静态方法。

### 优先级的问题

当一个类，既继承一个父类，又实现若干个接口时，父类中的成员方法与接口中的默认方法重名，子类就近选择执行父类的成员方法。

# static关键字

```java
public class Student {
    // 成员变量
    public String name;
    public char sex; // '男'  '女'
    public int age;

    // 无参数构造器
    public Student() {

    }
    
    // 有参数构造器
    public Student(String  a) {

    }
}
```

name ,age , sex确实是每个学生对象都应该有的属性，应该属于每个对象。

关于 `static` 关键字的使用，它可以用来修饰的成员变量和成员方法，

被static修饰的成员是**属于类**的是放在静态区中，

没有static修饰的成员变量和方法则是**属于对象**的。

我们上面案例中的成员变量都是没有static修饰的，所以属于每个对象。

![image-20210425145921071](https://gitee.com/qhzeng/markdown/raw/master/image/image-20210425145921071.png)

### 静态变量及其访问

有static修饰成员变量，说明这个<u>**成员变量是属于类的**</u>，这个成员变量称为**类变量**或者**静态成员变量**。 直接用  类名访问即可。因为类只有一个，所以静态成员变量在内存区域中也只存在一份。所有的对象都可以共享这个变量。

**格式：对象.实例成员变量`Student.name`**

### 静态方法及其访问

有static修饰成员方法，说明这个**<u>成员方法是属于类的</u>**，这个成员方法称为**类方法或者静态方法**。 直接用  类名访问即可。因为类只有一个，所以静态方法在内存区域中也只存在一份。所有的对象都可以共享这个方法。

与静态成员变量一样，静态方法也是直接通过

**格式：类名.方法名称`Student.study();`**  

## 小结

1.当 `static` 修饰成员变量或者成员方法时，该变量称为**静态变量**，该方法称为**静态方法**。该类的每个对象都**共享**同一个类的静态变量和静态方法。任何对象都可以更改该静态变量的值或者访问静态方法。但是不推荐这种方式去访问。因为静态变量或者静态方法直接通过类名访问即可，完全没有必要用对象去访问。

2.无static修饰的成员变量或者成员方法，称为**实例变量，实例方法**，实例变量和实例方法必须创建类的对象，然后通过对象来访问。

3.static修饰的成员**<u>属于类，会存储在静态区</u>**，是随着类的加载而加载的，且只加载一次，所以只有一份，节省内存。存储于一块固定的内存区域（静态区），所以，可以直接被类名调用。它优先于对象存在，所以，可以被所有对象共享。

4.无static修饰的成员，是属于对象，对象有多少个，他们就会出现多少份。所以必须由对象调用。





# 面向对象：多态



## 多态的形式

**多态是继封装、继承之后，面向对象的第三大特性。**

**多态是出现在继承或者实现implement关系中的**。

**多态体现的格式**：父类引用指向子类对象

```java
父类类型 变量名 = new 子类/实现类构造器;
变量名.方法名();
```

**多态的前提**：有继承关系，子类对象是可以赋值给父类类型的变量。例如Animal是一个动物类型，而Cat是一个猫类型。Cat继承了Animal，Cat对象也是Animal类型，自然可以赋值给父类类型的变量。

```java
public class Animal {  
    public void eat()｛
        System.out.println("动物吃东西！")
    ｝
}  

//子类

class Cat extends Animal {  
    public void eat() {  
        System.out.println("吃鱼");  
    }  
}  

class Dog extends Animal {  
    public void eat() {  
        System.out.println("吃骨头");  
    }  
}
public class Test {
    public static void main(String[] args) {
        // 多态形式，创建对象
        Animal a1 = new Cat();
        // 调用的是 Cat 的 eat
        a1.eat();

        // 多态形式，创建对象
        Animal a2 = new Dog();
        // 调用的是 Dog 的 eat
        a2.eat();
    }  
}
```



## 多态的定义和前提

**多态**： 是指同一行为，具有多个不同表现形式。

从上面案例可以看出，Cat和Dog都是动物，都是吃这一行为，但是出现的效果（表现形式）是不一样的。

 **前提【重点】**

1. 继承或者实现【二选一】

2. 方法的重写【意义体现：不重写，无意义】

3. 父类引用指向子类对象【格式体现】

   > 父类类型：指子类对象继承的父类类型，或者实现的父接口类型。



## 向上转型（自动转换）

**向上转型**：多态本身是子类类型向父类类型向上转换（自动转换）的过程，这个过程是默认的。
当父类引用指向一个子类对象时，便是向上转型。
使用格式：

```java
父类类型  变量名 = new 子类类型();
如：Animal a = new Cat();
```

## 向下转型（强制转换）

**向下转型**：父类类型向子类类型向下转换的过程，这个过程是强制的。
一个已经向上转型的子类对象，将父类引用转为子类引用，可以使用强制类型转换的格式，便是向下转型。

使用格式：

```java
子类类型 变量名 = (子类类型) 父类变量名;
如:Aniaml a = new Cat();
   Cat c =(Cat) a;  
```

##  instanceof 关键字

```java
变量名 instanceof 数据类型 
如果变量属于该数据类型或者其子类类型，返回true。
如果变量不属于该数据类型或者其子类类型，返回false。
```



# 内部类（需要用到的时候来查）

## 内部类的分类

按定义的位置来分

1. **静态内部类**，类定义在了成员位置 (类中方法外称为成员位置，有static修饰的内部类)
2. **实例内部内**，类定义在了成员位置 (类中方法外称为成员位置，无static修饰的内部类)
3. **局部内部类**，类定义在方法内
4. **匿名内部类**。一般定义在方法中，或者可执行代码中



## 静态内部类

**静态内部类特点**：

- 有static修饰的内部类，属于外部类本身的。
- 总结：静态内部类与其他类的用法完全一样。只是访问的时候需要加上外部类.内部类。
- **拓展**:静态内部类可以直接访问外部类的静态成员。

**内部类的使用格式**：

```
外部类.内部类。
```

**静态内部类对象的创建格式**：

```java
外部类.内部类  变量 = new  外部类.内部类构造器;
```

**案例演示**：



## 实例内部类

**实例内部类特点**：

- 无static修饰的内部类，属于外部类对象的。
- 宿主：外部类对象。

**内部类的使用格式**：

```java
 外部类.内部类。 // 访问内部类的类型都是用 外部类.内部类
```

**实例内部类创建对象格式**：

```
外部类.内部类 变量 = new 外部类构造器.new 内部类构造器;
```

- 拓展1：实例内部类不能定义静态成员。

- 拓展2：实例内部类可以直接访问外部类的私有和静态成员。

  **案例演示**

```java
public class InnerClassDemo02 {
    public static void main(String[] args) {
        //  宿主：外部类对象。
       // Outer02 out = new Outer02();
        // 创建内部类对象。
        Outer02.Inner02 in = new Outer02().new Inner02("张三");
        in.showName();
    }
}

class Outer02{

    // 实例内部类，属于外部类对象的。
    // 拓展：实例内部类不能定义静态成员。
    public class Inner02{
        // 这里面的东西与类是完全一样的。
        private String name;

        public Inner02(String name) {
            this.name = name;
        }

        public void showName(){
            System.out.println(this.name);
        }
    }
}
```

## 2.5 实例内部类面试题

请在?地方向上相应代码,以达到输出的内容

注意：内部类访问外部类对象的格式是：**外部类名.this**

```java
public class Demo05 {
    public static void main(String[] args) {
        Body.Heart heart = new Body().new Heart();
        heart.jump();
    }
}

class Body {	// 身体
    private int weight = 30;

    // 在成员位置定义一个类
    class Heart {
        private int weight = 20;

        public void jump() {
            int weight = 10;
            System.out.println("心脏在跳动 " + ?);	// 10
            System.out.println("心脏在跳动 " + ?);	// 20
            System.out.println("心脏在跳动 " + ?);	// 30
        }
    }
}
```

##  局部内部类

- **局部内部类** ：定义在**方法中**的类。只有在方法内才能使用

定义格式:

```java
class 外部类名 {
    数据类型 变量名;
	//在方法里边
	修饰符 返回值类型 方法名(参数列表) {
		// …
		class 内部类 {
			// 成员变量
			// 成员方法
		}
	}
}
```

## 匿名内部类【重点】

### 概述

**匿名内部类** ：是内部类的简化写法。它的本质是一个`带具体实现的` `父类或者父接口的` `匿名的` **子类对象**。
开发中，最常用到的内部类就是匿名内部类了。

### 匿名内部类前提和格式

匿名内部类必须**继承一个父类**或者**实现一个父接口**。



**匿名内部类格式**

```java
new 父类名或者接口名(){
    // 方法重写
    @Override 
    public void method() {
        // 执行语句
    }
};
```

###  使用方式

以接口为例，匿名内部类的使用，代码如下：

创建匿名内部类，并调用：GUI做界面

```java
interface Swim {
    public abstract void swimming();
}

public class Demo07 {
    public static void main(String[] args) {
        // 使用匿名内部类
		new Swim() {
			@Override
			public void swimming() {
				System.out.println("自由泳...");
			}
		}.swimming();

        // 接口 变量 = new 实现类(); // 多态,走子类的重写方法
        Swim s2 = new Swim() {
            @Override
            public void swimming() {
                System.out.println("蛙泳...");
            }
        };

        s2.swimming();
        s2.swimming();
    }
}
```

### 匿名内部类的特点

1. 定义一个没有名字的内部类
2. 这个类实现了父类，或者父类接口
3. 匿名内部类会创建这个没有名字的类的对象

### 匿名内部类的使用场景

通常在方法的形式参数是接口或者抽象类时，也可以将匿名内部类作为参数传递。代码如下：

```java
interface Swim {
    public abstract void swimming();
}

public class Demo07 {
    public static void main(String[] args) {
        // 普通方式传入对象
        // 创建实现类对象
        Student s = new Student();
        
        goSwimming(s);
        // 匿名内部类使用场景:作为方法参数传递
        Swim s3 = new Swim() {
            @Override
            public void swimming() {
                System.out.println("蝶泳...");
            }
        };
        // 传入匿名内部类
        goSwimming(s3);

        // 完美方案: 一步到位
        goSwimming(new Swim() {
            public void swimming() {
                System.out.println("大学生, 蛙泳...");
            }
        });

        goSwimming(new Swim() {
            public void swimming() {
                System.out.println("小学生, 自由泳...");
            }
        });
    }

    // 定义一个方法,模拟请一些人去游泳
    public static void goSwimming(Swim s) {
        s.swimming();
    }
}
```































































# 包和权限

|                  | public | protected | 缺省（空的） | private |
| ---------------- | ------ | --------- | ------------ | ------- |
| 同一类中         | √      | √         | √            | √       |
| 同一包中的类     | √      | √         | √            | ×       |
| 不同包的子类     | √      | √         | ×            | ×       |
| 不同包中的无关类 | √      | ×         | ×            | ×       |

可见，public具有最大权限。private则是最小权限。

编写代码时，如果没有特殊的考虑，建议这样使用权限：

- 成员变量使用`private` ，隐藏细节。
- 构造方法使用` public` ，方便创建对象。
- 成员方法使用`public` ，方便调用方法。

> 小贴士：不加权限修饰符，就是default权限集合



# Collection

* **集合**：集合是java中提供的一种容器，可以用来存储多个数据。

集合与数组的区别：

* 数组的长度是固定的（数组一旦定义了，就不能再修改数组的长度）。

  集合的长度是可变的（可以不断往集合添加元素）。

* 数组中存储的是同一类型的元素，可以存储任意类型数据。

  集合存储的都是引用数据类型。如果想存储基本类型数据需要存储对应的包装类型。（String Integer...）



<img src="https://gitee.com/qhzeng/markdown/raw/master/image/Collection%E9%9B%86%E5%90%88%E4%BD%93%E7%B3%BB%E5%9B%BE.jpg" alt="Collection集合体系图" style="zoom: 67%;" />

##  Collection 常用方法

Collection是所有单列集合的父接口，因此在Collection中定义了单列集合(List和Set)通用的一些方法，这些方法可用于操作所有的单列集合。方法如下：

* `public boolean add(E e)`：  把给定的对象添加到当前集合中 。(返回值为Boolean，通常都是true)
* `public boolean remove(E e)`: 把给定的对象在当前集合中删除。
* `public void clear()` :清空集合中所有的元素。(元素被清空了，但是集合还在)
* `public boolean contains(Object obj)`: 判断当前集合中是否包含给定的对象。
* `public boolean isEmpty()`: 判断当前集合是否为空。
* `public int size()`: 返回集合中元素的个数。
* `public Object[] toArray()`: 把集合中的元素，存储到数组中

# 迭代器Iterator



## Iterator接口

在程序开发中，经常需要遍历集合中的所有元素。针对这种需求，JDK专门提供了一个接口`java.util.Iterator`。

想要遍历Collection集合，那么就要获取该集合迭代器完成迭代操作，下面介绍一下获取迭代器的方法：

* `public Iterator iterator()`: 获取集合对应的迭代器，用来遍历集合中的元素的。

迭代的概念：

* **迭代**：即Collection集合元素的通用获取方式。在取元素之前先要判断集合中有没有元素，如果有，就把这个元素取出来，继续在判断，如果还有就再取出出来。一直把集合中的所有元素全部取出。这种取出方式专业术语称为迭代。

Iterator接口的常用方法如下：

* `public E next()`:返回迭代的下一个元素。

* `public boolean hasNext()`:如果仍有元素可以迭代，则返回 true。

  

![image-20210501135242243](https://gitee.com/qhzeng/markdown/raw/master/image/image-20210501135242243.png)





### 迭代器的使用步骤

1.使用集合中的方法Iterator()获取迭代器的实现类对象，使用Iterator接口接收（多态）

2.使用Iterator接口中的方法hasNext判断是否还有下一个元素

3.使用Iterator接口中的next方法取出集合中的下一个元素

<img src="https://gitee.com/qhzeng/markdown/raw/master/image/image-20210501140338149.png" alt="image-20210501140338149" style="zoom:50%;" />



## 增强For循环

用来遍历集合和数组



格式：for(数组的数据类型 变量名: 集合名/数组名){

​				sout(变量名)}

```java
 public static  void demo02(){
        Collection<String> collection =new ArrayList<>();
        collection.add("AAA");
        collection.add("BBB");
        for (String s :
                collection) {
            System.out.print(s);
        }
        }
    public  static  void demo01(){
        int [] arr={1,2,3,4,5,6};
        for (int i : arr) {
            System.out.print(i);
        }
    }
```



# List接口

Collection中的常用几个子类（`java.util.List`集合、`java.util.Set`集合）。

##  List接口介绍

`java.util.List`接口继承自`Collection`接口，是单列集合的一个重要分支，习惯性地会将实现了`List`接口的对象称为List集合。

在List集合中允许出现重复的元素，所有的元素是以一种线性方式进行存储的，在程序中可以通过索引来访问集合中的指定元素。另外，List集合还有一个特点就是元素有序，即元素的存入顺序和取出顺序一致。

## List接口三大特点：

1. 它是一个元素存取**有序的集合**。例如，存元素的顺序是11、22、33。那么集合中，元素的存储就是按照11、22、33的顺序完成的）。
2. 它是一个**<u>带有索引</u>**的集合，**通过索引就可以精确的操作集合中的元素**（与数组的索引是一个道理）。
3. 集合中**<u>可以有重复的元素</u>**，通过元素的equals方法，来比较是否为重复的元素。

## List接口中常用方法

List作为Collection集合的子接口，不但继承了Collection接口中的全部方法，而且还增加了一些根据元素索引来操作集合的特有方法，如下：

- `public void add(int index, E element)`: 将指定的元素，添加到该集合中的指定位置上。
- `public E get(int index)`:返回集合中指定位置的元素。
- `public E remove(int index)`: 移除列表中指定位置的元素, 返回的是被移除的元素。
- `public E set(int index, E element)`:用指定元素替换集合中指定位置的元素,返回值的更新前的元素。



## ArrayList集合

`java.util.ArrayList`集合数据存储的结构是数组结构。元素增删慢，查找快，由于日常开发中使用最多的功能为查询数据、遍历数据，所以`ArrayList`是最常用的集合。

```java
boolean add(E e) 
//将指定的元素列表的结束。      
void clear() 
//从这个列表中移除所有的元素。  
E get(int index) 
//返回此列表中指定位置的元素。  
E remove(int index) 
//移除此列表中指定位置的元素。  
int size() 
//返回此列表中元素的数目。  
```



```java
for (int i = 0; i < arrayList.size(); i++) {
            System.out.println(arrayList.get(i));
            
        }
```



## LinkedList集合

`java.util.LinkedList`集合数据存储的结构是链表结构。方便元素添加、删除的集合。

> LinkedList是一个双向链表，那么双向链表是什么样子的呢，我们用个图了解下

实际开发中对一个集合元素的添加与删除经常涉及到首尾操作，而LinkedList提供了大量首尾操作的方法。这些方法我们作为**了解即可**：

- `public void addFirst(E e)`:将指定元素插入此列表的开头。
- `public void addLast(E e)`:将指定元素添加到此列表的结尾。
- `public E getFirst()`:返回此列表的第一个元素。
- `public E getLast()`:返回此列表的最后一个元素。
- `public E removeFirst()`:移除并返回此列表的第一个元素。
- `public E removeLast()`:移除并返回此列表的最后一个元素。
- `public E pop()`:从此列表所表示的堆栈处弹出一个元素。
- `public void push(E e)`:将元素推入此列表所表示的堆栈。
- `public boolean isEmpty()`：如果列表不包含元素，则返回true。

LinkedList是List的子类，List中的方法LinkedList都是可以使用，这里就不做详细介绍，我们只需要了解LinkedList的特有方法即可。在开发时，LinkedList集合也可以作为堆栈，队列的结构使用。





# Set接口

`java.util.Set`接口和`java.util.List`接口一样，同样继承自`Collection`接口，它与`Collection`接口中的方法基本一致，并没有对`Collection`接口进行功能上的扩充，只是比`Collection`接口更加严格了。与`List`接口不同的是，`Set`接口都会以某种规则保证存入的元素不出现重复。

`Set`集合有多个子类，这里我们介绍其中的`java.util.HashSet`、`java.util.LinkedHashSet`、`java.util.TreeSet`这两个集合。

## Set接口的特点

- 不允许存储重复的元素
- 没有索引，没有带索引的放啊，也不能使用普通的for循环，可以使用迭代器，增强for

## HashSet集合介绍

`java.util.HashSet`是`Set`接口的一个实现类，它所存储的元素是不可重复的，并且元素都是无序的(即存取顺序不能保证不一致)。`java.util.HashSet`底层的实现其实是一个`java.util.HashMap`支持，由于我们暂时还未学习，先做了解。

`HashSet`是根据对象的哈希值来确定元素在集合中的存储位置，因此具有良好的存储和查找性能。保证元素唯一性的方式依赖于：`hashCode`与`equals`方法。



## HashSet特点

- 不允许存储重复的元素
- 没有索引，没有带索引的放啊，也不能使用普通的for循环，可以使用迭代器，增强for
- 是一个无序的集合，存储元素和取出元素的顺序有可能不一致
- 底层是一个哈希表结构（查询速度非常块）

我们先来使用一下Set集合存储，看下现象，再进行原理的讲解:

```java
public class HashSetDemo {
    public static void main(String[] args) {
        //创建 Set集合
        HashSet<String>  set = new HashSet<String>();

        //添加元素
        set.add(new String("cba"));
        set.add("abc");
        set.add("bac"); 
        set.add("cba");  
        //遍历
        for (String name : set) {
            System.out.println(name);
        }
    }
}
```

输出结果如下，说明集合中不能存储重复元素：

```
cba
abc
bac
```

> tips:根据结果我们发现字符串"cba"只存储了一个，也就是说重复的元素set集合不存储。

##  HashSet集合存储数据的结构（哈希表）

在**JDK1.8**之前，哈希表底层采用数组+链表实现，即使用数组处理冲突，同一hash值的链表都存储在一个数组里。但是当位于一个桶中的元素较多，即hash值相等的元素较多时，通过key值依次查找的效率较低。而

**JDK1.8**后，哈希表存储采用数组+链表+红黑树实现，当链表长度超过阈值（8）时，将链表转换为红黑树，这样大大减少了查找时间。<img src="https://gitee.com/qhzeng/markdown/raw/master/image/%E5%93%88%E5%B8%8C%E8%A1%A8.png" alt="哈希表" style="zoom: 80%;" />

<u>**JDK1.8**引入红黑树大程度优化了HashMap的性能，那么对于我们来讲保证HashSet集合元素的唯一，其实就是根据对象的hashCode和equals方法来决定的。如果我们往集合中存放自定义的对象，那么保证其唯一，就必须复写hashCode和equals方法建立属于当前对象的比较方式。</u>



## LinkedHashSet

我们知道HashSet保证元素唯一，可是元素存放进去是没有顺序的，那么我们要保证有序，怎么办呢？

在HashSet下面有一个子类`java.util.LinkedHashSet`，它是链表和哈希表组合的一个数据存储结构。**（数组+链表+红黑树   额外加了一条链表）**

**注意：这里的顺序指的是add的顺序，并非数据的顺序**

演示代码如下:

```java
public class LinkedHashSetDemo {
	public static void main(String[] args) {
		Set<String> set = new LinkedHashSet<String>();
		set.add("bbb");
		set.add("aaa");
		set.add("abc");
		set.add("bbc");
        Iterator<String> it = set.iterator();
		while (it.hasNext()) {
			System.out.println(it.next());
		}
	}
}
结果：
  bbb
  aaa
  abc
  bbc
```





# 可变参数

- 可变参数：是JDK1.5之后出现的新特性

  使用前提：当方法的参数列表数据类型已经确定，但是参数的个数不确定，就可以使用可变参数

- 使用格式：定义方法时使用

  `修饰符 返回值类型 方法名 （数据类型...变量名）{}`

- 可变参数的原理：

  可变参数的底层就是一个数组，更具传递参数个数不同，会创建不同长度的数组，来存储这些参数传递的参数个数，可以是0个(不传递)

- **注意：**

- **一个方法之能有一个可变参数**

- **如果一个参数列表有多个参数，那么可变参数写在最后面**



```java
public class Array {
    public static void main(String[] args) {
        int i =add(1,2,3,4,5);
        System.out.println(i);
    }
    public static int add(int...arr){
        int sum=0 ;
        for (int i : arr) {
            sum =sum+ i;
        }

        return sum;
    }
    public static int add(int a,int b, int c){
        return a+b+c;
    }
}
```



# Collections常用功能

- `java.utils.Collections`是集合工具类，用来对集合进行操作。

  常用方法如下：

- `public static void shuffle(List<?> list) `:打乱集合顺序。

- `public static <T> void sort(List<T> list)`:将集合中元素按照默认规则排序。

- `public static <T> void sort(List<T> list，Comparator<? super T> )`:将集合中元素按照指定规则排序。

代码演示：

```java
public class CollectionsDemo {
    public static void main(String[] args) {
        ArrayList<Integer> list = new ArrayList<Integer>();
   
        list.add(100);
        list.add(300);
        list.add(200);
        list.add(50);
        //排序方法 
        Collections.sort(list);
        System.out.println(list);
    }
}
结果：
[50,100, 200, 300]
```





<img src="https://gitee.com/qhzeng/markdown/raw/master/image/image-20210502025358164.png" alt="image-20210502025358164" style="zoom: 80%;" />



