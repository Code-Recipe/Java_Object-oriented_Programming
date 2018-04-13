继承
======
继承是Java中非常重要的一个概念。继承反应的是类和类之间的一个关系。还记得在第一章节中，我们提到，类可以具有方法和属性吗？继承，实际上说的就是，"子类"可以继承"父类"的属性，或者是方法。通过继承，可以让信息以一种层级的关系进行管理。

接下来，开始探索继承王国吧！💖

父类和子类的关系
------
一个由其他的类派生出来的类，叫做子类(subclass)，而派生出子类的类，则叫做父类（superclass或parent class)。子类包含着父类的所有属性和方法，同时，子类还可以具有自己独有的属性和方法，因此，子类可以包含着比父类更多的属性和方法！

在Java中，除了最终超类：Object类，所有的类都有且仅有一个直接的父类（这被称为单继承）。当没有明确在程序中声明某些类所属的父类时，这些类都是最终超类：Object类的（隐式）子类。

类可以层层继承，也就是说，A类可以继承自B类，而B类又继承自C类，C类又有D类派生而来（也就是说，C类又继承自D类），等等等等，子子孙孙无穷尽也。最终，就如同基因学上，所有的人类都来自于"Y染色体亚当"和"X染色体夏娃"一样，层层推溯以后，所有的类都最终派生于一个"终极(topmost)"类，也就是最终超类：Object类。我们可以用树的枝桠来形容，这棵树，我们叫它"继承树"。Object类，作为最终超类，就是这棵树最底层的那个"万物之源"。

继承的概念是简单而强大的。当你想创建一个新的类，而此时已经有既成的一个类包含了你想要的一些信息（也就是描述方法或属性的代码），你就可以直接在已经存在的类的基础上，派生出一个新的类，让那个派生出来的新类，来继承旧类的属性和方法。在这样的过程中，我们可以避免重复编写与调试已经写过的类中的代码，也就是程序员常说的"避免重复造轮子"。

继承为代码重用提供了一个有效的机制。 假设父类的代码已经过测试和调试，那么，由于子类对象继承了父类，那么子类也就共享父类的代码，因此唯一需要的测试和调试的新代码就是用于子类的独特代码。

说了这么多，那么，如何实现继承呢？


实现继承
------
为了具体地实现继承，有两个非常重要的Java关键字需要掌握：一个是"extends"，一个是"implements"。其中，"extends"是专门为类准备的，"implements"是专门为接口（后续会讲到）来准备的。

在这里，我们讲一下类与接口有什么区别。类有自己的属性（状态）和方法，有具体行为的一个实现。而接口实际上只定义了用于实现接口的类，需要去具备怎样的行为，但具体这个行为怎样去实现，并不用去关心。就好像，如果我是一个接口，下雨了，我说，我要一把伞，然后我就得到了一把伞；但具体这把伞怎么设计，怎么制造，我毫不关心。但如果我是一个方法，我就必须要详细设计出这把伞，把它制造出来，对这把伞的底细摸得清清楚楚。

说了这么多，有些抽象，让我们用一个具体的例子来作比喻吧。
比方说，我现在有一只狗，和一只鳄鱼，前者是哺乳动物，后者是爬行动物。但两者都会游泳，也就是说，两者都具有"游泳"这个行为（方法），并且两者都有需要共同的属性，例如具有耳朵、眼睛，和腿。如果我们分别去定义这些属性，则会造成代码的冗余、效率的低下。所以，我们可以将这些属性进行相应的抽象，定义一个哺乳动物类、爬行动物类，二者都属于动物类。把大家共有的属性：耳朵、眼睛、腿，都定义在动物类中。而狗和鳄鱼都会游泳，但二者的游泳方式不同，故我们可以将两种方式分别定义在哺乳动物类和爬行动物类中。

整个继承的框架，是这样的：
```Java
// 动物
class Animal {
}

// 哺乳动物
class Mammal extends Animal{
}

// 爬行动物
class Reptile extends Animal{
}

// 狗
class Dog extends Mammal{
}
```
上面我们描述的例子，具体完整的代码实现如下：
```Java
// 动物
class Animal {
   int eyes;
   public void run(){
      System.out.println("I can run.")
    }
}

// 哺乳动物
class Mammal{

}

//狗
public class Dog extends Mammal{
  public void info(){
    System.out.println("I have " + eyes + "eyes.")
  }

  public static void main(String[] args){
    Dog myDog = new Dog();
    myDog.eyes = 2;
    myDog.run();
  }
}

// 爬行动物
class Reptile extends Animal{
}
```
我们可以看见，哺乳动物类、爬行动物类、狗类，都继承自动物类。因此，动物类所定义的属性、行为，如眼睛、跑，在所有的子类都有所继承。因此，在狗类中，我们就不用再去重复定义眼睛、跑了，并且在狗类中，我们可以直接调用父类的行为、属性。而info()行为是Dog自己的行为，因此我们需要在Dog类中单独进行声明。我们可以看出：假如有两个类，A与B，而A派生出B，换句话说，B继承自A，则：
```Java
class A{

}

class B extends A{

}
```
让我们再来看一个例子：


我们定义一个类：自行车
```java
public class Bicycle {

    // 这个自行车有三个属性
    public int cadence;
    public int gear;
    public int speed;

    // 这个自行车类有一个构造方法
    public Bicycle(int startCadence, int startSpeed, int startGear) {
        gear = startGear;
        cadence = startCadence;
        speed = startSpeed;
    }

    // 这个自行车有四个方法
    public void setCadence(int newValue) {
        cadence = newValue;
    }

    public void setGear(int newValue) {
        gear = newValue;
    }

    public void applyBrake(int decrement) {
        speed -= decrement;
    }

    public void speedUp(int increment) {
        speed += increment;
    }

}
```

然后我们再定义一个类：山地自行车。

显然，山地自行车也属于自行车。
```Java
public class MountainBike extends Bicycle {

    // 山地自行车有自己的一个特有属性
    public int seatHeight;

    // 山地自行车子类有一个构造方法
    public MountainBike(int startHeight,
                        int startCadence,
                        int startSpeed,
                        int startGear) {
        super(startCadence, startSpeed, startGear);
        seatHeight = startHeight;
    }   

    // 山地自行车v子类有自己的一个特有方法
    public void setHeight(int newValue) {
        seatHeight = newValue;
    }   
}
```

我们可以看到，山地自行车继承了自行车通用的所有属性(cadence, speed, gear)，而其自己特有的属性为seatHeight（座椅高度）。我们可以看见，在山地自行车类中，可以直接使用父类（自行车类）的所有属性。super关键字的用法，我们会在下一章节提到。同学们可以先猜一猜，super关键字起到了什么样的作用。

instanceof关键字
-----
我们可以通过instanceof关键字判断父类与子类是否存在继承的关系。instanceof 是 Java 的保留关键字，它的作用是测试它左边的对象是否是它右边的类的实例，或左边的类是否由继承自右边的类。用来判断哺乳动物是否是动物，狗是否是动物等，如果是那么就是真，否则就是假，instanceof关键字返回 boolean 的数据类型。


例如：
```java
  
public class Vehicle {   

}  

public class Bicycle extends Vehicle{
    public static void main(String[] args) {
        system.out.println(Bicycle instanceof      Vehicle); // 输出结果为：ture  

    }  
}
```




方法重写
-----
方法重写(Method override)指的是，如果一个类继承了其父类的方法，那么我们可以通过方法重写，用同名的方法，来"覆盖"掉所继承的父类的对应方法。相当于，在子类中我们"重新写了"一次，父类中该名称的方法，并用此方法来替代所继承的同名方法。

方法重写带来的好处是：我们能够定义特定于子类类型的行为，这意味着子类可以根据其各自的特殊要求，来实现父类方法，而无需修改父类代码。

重写的方法具有与父类的方法相同的名称，参数的数量和类型，以及返回类型与其覆盖的方法相同。 

请看如下两个类。第一个类是动物类，包含着一个实例方法，以及一个静态方法（类方法）。第二个类是第一个类（动物类）的子类：猫类。

**请注意，以上指的是实例方法(Instance method)的方法重写。对于静态方法（类方法），不存在方法重写，而是方法隐藏(Method hiding)**

如果一个子类在超类中定义了一个与静态方法具有相同名称的静态方法，那么子类中的方法隐藏超类中的方法。

隐藏静态方法和重写实例方法之间的区别是：

被真正调用的重写实例方法，是子类中"重写"出来的那一个。而真正被调用的隐藏静态方法，取决于它是从父类还是子类中被调用。


```java
public class Animal {
    public static void testClassMethod() {
        System.out.println("The static method in Animal");
    }
    public void testInstanceMethod() {
        System.out.println("The instance method in Animal");
    }
}


public class Cat extends Animal {
    public static void testClassMethod() {
        System.out.println("The static method in Cat");
    }
    public void testInstanceMethod() {
        System.out.println("The instance method in Cat");
    }

    public static void main(String[] args) {
        Cat myCat = new Cat();
        Animal myAnimal = myCat;
        Animal.testClassMethod();
        myAnimal.testInstanceMethod();
    }
}
```
Cat类覆盖Animal类中的实例方法并隐藏Animal中的静态方法。 此类中的主要方法创建Cat的一个实例对象。

然后，在Cat类的main()方法中调用了Cat类的静态方法:testClassMethod()，以及myAnimal这一个对象的实例方法:testInstanceMethod()。 


注意，被调用的实例方法testInstanceMethod()是被子类重写出来的那一个，而被调用的静态方法，则取决于调用这个方法的类是父类还是子类；在这一个例子中，是Animal类的，而不是Cat类中的。

这个程序编译运行结果是：
```
The static method in Animal
The instance method in Cat
````
正如所说的的那样，被调用的隐藏静态方法的版本是调用它的类中中的那一个，被调用的重写实例方法，则是子类中的那一个。

如果我们把
```java
        Animal.testClassMethod();
```
改成
```java
        Cat.testClassMethod();
```
会发生什么呢？

来试试看！

<lab lang="java" parameters="filename=Cat.java">
<notice>练习环境在此无法显示，请移步至[程谱 coderecipe.cn](https://coderecipe.cn/learn/1)查看。</notice>
public class Animal {
    public static void testClassMethod() {
        System.out.println("The static method in Animal");
    }
    public void testInstanceMethod() {
        System.out.println("The instance method in Animal");
    }
}


public class Cat extends Animal {
    public static void testClassMethod() {
        System.out.println("The static method in Cat");
    }
    public void testInstanceMethod() {
        System.out.println("The instance method in Cat");
    }

    public static void main(String[] args) {
        Cat myCat = new Cat();
        Animal myAnimal = myCat;
        Cat.testClassMethod();
        myAnimal.testInstanceMethod();
    }
}
</lab>

```java
class Human{
   //被重写的方法
   public void eat()
   {
      System.out.println("Human is eating");
   }
}
class Boy extends Human{
   //重写的同名新方法
   public void eat(){
      System.out.println("Boy is eating");
   }
   public static void main( String args[]) {
      Boy obj = new Boy();
      //这会调用子类中重写的eat()方法
      obj.eat();
   }
}
```
现在，大家对上面这段代码的运行结果是
```Boy is eating```而非```Human is eating```的原因，已经能够完全理解了吧！

**注意：**

* **私有的(private)、静态的(static)、最终的(final)方法是不可以被重写的，因为他们的作用于是局部的(local)而非全局的。然而，静态方法可以在子类中重新声明(re-declare)，在这种情况下，子类方法的行为将会不同，并且与父类的相同静态方法无关，父类的静态方法相当于在子类中，被隐藏了。**

* **重写方法的参数列表（子类的方法）必须与重写方法（父类的方法）相匹配。参数的数据类型及其顺序应完全匹配。**

抽象类
-----

