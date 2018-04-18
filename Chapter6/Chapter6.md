接口
=====
大家已经顺利完成了前几章的学习，Java最困难也是最核心的几章大家都已经克服啦。接下来，继续一往直前，开始探索接口王国吧！💖

接口是什么
-----
很多时候，在开发软件的过程中，对于不同的组、甚至是不同机构组织的程序员群体，同意签署一份说明软件如何交互的“合同”是很重要。这样一来，各个组间的代码可以互相交互，而完全不需要知道如何其他组的代码具体是如何实现的，也就是"会用就好，不需要在意具体如何实现"。接口就是这样的"合同"。

想象一下，在一个未来的社会，电脑控制的自动驾驶汽车，在没有人类司机的情况下载着乘客穿过大街小巷。汽车制造商通过Java编写控制汽车停止，启动，加速，左转等等行为的软件。而另有专门的自动驾驶仪制造商B，为汽车制造商生产的自动驾驶汽车提供自动驾驶仪，通过GPS、陀螺仪提供的数据来自动驾驶汽车。相当于，汽车制造商制造了一具身体（汽车），以及声明了这一具身体如何能够被控制着移动（就好像人的肢干可以运动，汽车可以前进后退一样），而自动驾驶仪制造商为车辆提供了大脑。

那么，汽车制造商组成的商业联盟必须发布行业标准接口，详细说明可以调用哪些方法使汽车行驶。所有的汽车制造商都使用这一个公认的行业标准，然后指导自动驾驶仪制造商，如何调用接口中描述的方法来使得"大脑"——自动驾驶仪，去指挥"身体"——车辆的运动。其他的工业组织，例如自动驾驶仪制造商，都不需要知道汽车制造商的软件（汽车如何运动）具体是如何实施的。事实上，每个制造商（例如汽车制造商，自动驾驶仪制造商）都认为它的软件是高度专有的，他们各自提供了接口，给别的制造商进行对接，但具体实现这些方法的过程，则是各自不透露的。

在Java编程语言中，接口是一个引用类型，类似于一个类，它相当于是一类方法的集合（有点像抽象类）。在接口中，这些方法，就如同抽象类一样，可以是抽象的（只包含一个声明，却不包括具体实现），也可以是普通的实例方法或静态方法（包括具体方法的实现）。 也就是说，对于接口，方法体只存在于普通的实例方法或静态方法中。 接口不能被实例化 - 它们只能由类实现或由其他接口扩展。

在AP考试中，普通的实例方法或静态方法（带具体方法实现的）是不会被考察的。只有抽象的接口会被考察。这也是我们本章设计的范围。

定义接口
-----
就像我们定义一个类一样，我们也需要先去定义一个接口，才能够使用它。
当我们定义一个类时，我们使用的关键字是`class`。而对于接口，我们使用的关键字是`interface`。例如：

```java
public interface SwimmingObject
{
    void swim();
    //method that simulates swimming of object
    boolean isSwimming(); //true if object is swimming, false otherwise
}
```
在这个例子中，我们定义了两个抽象方法：没有返回值的`swim()`和返回值为布尔型的`isSwimming()`
`public`访问修饰符表明，这一个接口可以被所有包(package)中的所有类调用。如果我们没有显式地声明一个接口是`public`的，那么这个接口就只能这个接口所在的包中的类调用。

接口与接口间也可以存在继承关系，从而扩展其他的接口，就如同一个子类可以继承父类从而扩展父类的内容一样。
但是，一个类只能直接继承自一个父类，不可能出现一个类同时直接继承自很多个父类的情况。(单继承)
而一个接口可以扩展任意数量的接口，我们使用英文逗号`,`来分隔开继承自的多个接口。如:
```java
public interface ExampleInterface extends Interface1, Interface2, Interface3
```
实现接口
-----
我们已经学会了如何定义接口，那么，我们如何让类去使用已经定义好的接口，或者说，我们如何把类"接上"这些接口呢？答案是：使用`implement`关键字。例如：

```java
public class Fish implements SwimmingObject{
//类的内容
}
```
这样一来，我们的类`Fish`就使用了`SwimmingObject`接口，也就"接上了"这个接口所提供的所有方法。因此，我们的类中，无论是否有定义新的方法，都一定会带有`SwimmingObject`接口中的两个方法：`swim()`与`isSwimming`()。

注意，继承自类`Fish`的所有子类都会自动地与父类`Fish`一样，接入`SwimmingObject`接口。父类`Fish`中带有了来自接口`SwimmingObject`的两个方法：``swim()`与`isSwimming`()， 继承自该类的子类也必然带有这样的两个方法。

假如父类没有接入一个接口，也可以单独为子类接入一个接口，例如：
```java
public class Sardine extends Fish implements SwimmingObject
{
//类的内容
}
```

**注意：在这样使用时，`extends`关键字必须出现在implement关键词之前。**

前面我们提到，一个类只能直接继承自一个父类，不可能出现一个类同时直接继承自很多个父类的情况。而一个接口可以扩展任意数量的接口。同样的，一个类只能直接继承自一个父类，却可以同时接上多
个不同的接口，例如：
```java
public class SubClass extends SuperClass implements Interface1, Interface2, ...
```

抽象类与接口的区别
-----
抽象类与接口相似。二者都不能被实例化，并可能都包含了一系列方法（或具体或抽象）（在接口中使用具体的方法是Java 8中的新特性，一般而言接口只提供抽象的方法，具体的方法AP不考察）。然而，在接口中是不可以定义实例变量的，而在抽象类中可以。并且，一个类只能继承一个直接父类，这个父类可以是具体的类也可是抽象类；但是一个类可以接上多个接口。抽象类中的方法可以是各种类型的，而接口中的成员变量只能是`public static final`类型的。

抽象类是对一种事物的抽象，即对类抽象，而接口是对行为的抽象。抽象类是对整个类整体进行抽象，包括属性、行为，但是接口却是针对类的行为（方法）进行抽象，而不包括属性（接口中不能定义实例变量）。

当一种方法，对于正在编写的程序来说是非常适用的，但这种方法同时对其他的程序也同样适用时，我们就可以考虑使用接口。

小练习
-----
1. Which statement about abstract classes and interfaces is false?

(A) An interface cannot implement any non-default instance methods, whereas
an abstract class can.

(B) A class can implement many interfaces but can have only one superclass.

(C) An unlimited number of unrelated classes can implement the same interface.

(D) It is not possible to construct either an abstract class object or an interface
object.

(E) All of the methods in both an abstract class and an interface are public.

<cr type="hidden"><notice>隐藏内容功能在此无法正常显示，请移步至[程谱 coderecipe.cn](https://coderecipe.cn/learn/3)查看。</notice>E</cr>

在这里练习吧：
<lab lang="java" parameters="filename=Hello.java">
<notice>练习环境在此无法显示，请移步至[程谱 coderecipe.cn](https://coderecipe.cn/learn/3)查看。</notice>
public class Hello {
   public static void main(String[] args) {
     // 在这里添加你的代码
   }
}
</lab>
