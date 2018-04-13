多态
======
初识多态
-----
这一小节中，我们将阐述多态的概念。若大家觉得有些晦涩，也没有关系，可以边看边思考。在有了这一小节的初步印象后，下一小节将会帮助大家更好地理解多态的概念。

多态(Polymorphism)是Java面向对象编程中非常重要的一个概念。多态，原本指的是在生物学中，一个生物体或物种，可以有不同的形态或发育阶段（例如蝴蝶的变态）。**在Java中，多态指的是，同一个方法具有多个不同表现形式或形态的能力。**
多态的好处是，可以使程序有良好的扩展，并可以对所有类的对象进行通用处理。

多态的概念，与前一节我们讲过的`方法重写`有着紧密的关联。一个至少在一个子类中被重写过的方法，就被称为是多态的方法。

对于被重写过的方法，它们都具有相同的方法名。那么Java在运行的时候，该如何是好？Java是依靠什么机制，来选择具体要执行哪一个方法的呢？

**在Java中，方法调用总是由调用这一方法的对象实际指向的对象类型（也就是在`new`语句后紧跟着的类型），而不是由这一对象引用的对象类型（也就是在`new`语句中，实际对象前面的那个类型）来决定的。**


例如，在语句
```javav
Animal puppy = new Dog();
```
中，实例对象`puppy`所引用的类型是`Animal`，而其实际指向的类型则是`Dog`。

这个机制，就叫做多态。

**多态是一个为处在类继承层次结构中的特定对象，选择适当的方法的机制。**

来给大家举一个例子。这个例子比较长，但在其后有详细的解释，不要慌！
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
    
    public void printDescription(){
        System.out.println("\nBike is " + "in gear " + this.gear
        + " with a cadence of " + this.cadence +
        " and travelling at a speed of " + this.speed + ". ");
    }
}

public class MountainBike extends Bicycle {
    private String suspension;

    public MountainBike(
               int startCadence,
               int startSpeed,
               int startGear,
               String suspensionType){
    }

    public void printDescription() {
        super.printDescription();
        System.out.println("The " + "MountainBike has a" +
            getSuspension() + " suspension.");
    }
} 


public class RoadBike extends Bicycle{
    private int tireWidth;

    public RoadBike(int startCadence,
                    int startSpeed,
                    int startGear,
                    int newTireWidth){
    }

    public void printDescription(){
        super.printDescription();
        System.out.println("The RoadBike" + " has " + getTireWidth() +
            " MM tires.");
    }
}

public class TestBikes {
  public static void main(String[] args){
    Bicycle bike01, bike02, bike03;

    bike01 = new Bicycle(20, 10, 1);
    bike02 = new MountainBike(20, 10, 5, "Dual");
    bike03 = new RoadBike(40, 20, 8, 23);

    bike01.printDescription();
    bike02.printDescription();
    bike03.printDescription();
  }
}
```

下面进行拆分解释。首先，如下是我们在上一节中见过的Bicycle类，为了展示多态，我们引入一个方法`printDescription`，来展示一个对象（自行车）的所有当前属性。最终`Bicycle`类为如下：
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
    
    public void printDescription(){
        System.out.println("\nBike is " + "in gear " + this.gear
        + " with a cadence of " + this.cadence +
        " and travelling at a speed of " + this.speed + ". ");
}
}
```


为了展示多态，我们由`Bicycle`类派生出`MountainBike`类与`RoadBike`类，并在二者中重写`printDescription`方法。

在`MountainBike`类中，我们引入一个新的属性：`suspension`，来描述山地自行车的悬挂缓冲系统（描述这辆车是否有一个前缓冲系统`Front`，或有一个前缓冲系统和一个后缓冲系统`Dual`）.
```java
public class MountainBike extends Bicycle {
    private String suspension;

    public MountainBike(
               int startCadence,
               int startSpeed,
               int startGear,
               String suspensionType){
    }

    public void printDescription() {
        super.printDescription();
        System.out.println("The " + "MountainBike has a" +
            getSuspension() + " suspension.");
    }
} 

```
请注意重写的`printDescription`方法。 除了之前提供的信息之外，输出中还包括有关悬挂缓冲系统的其他信息。

接下来，创建`RoadBike`类。 由于公路赛车或赛车有较细窄的轮胎，因此我们添加一个属性`tireWidth`来描述轮胎宽度。
```java
public class RoadBike extends Bicycle{
    private int tireWidth;

    public RoadBike(int startCadence,
                    int startSpeed,
                    int startGear,
                    int newTireWidth){
    }

    public void printDescription(){
        super.printDescription();
        System.out.println("The RoadBike" + " has " + getTireWidth() +
            " MM tires.");
    }
}
```
请注意，`printDescription`方法再次被重写。 除了`Bicycle`具有的属性外，这里还显示有关轮胎宽度的信息。

总而言之，我们有三类：父类`Bicycle`，以及并列的子类`MountainBike`和`RoadBike`。 这两个子类重写`printDescription`方法并打印各自不同的信息。

接着，我们写一个`TestBikes`类进行测试。
```java
public class TestBikes {
  public static void main(String[] args){
    Bicycle bike01, bike02, bike03;

    bike01 = new Bicycle(20, 10, 1);
    bike02 = new MountainBike(20, 10, 5, "Dual");
    bike03 = new RoadBike(40, 20, 8, 23);

    bike01.printDescription();
    bike02.printDescription();
    bike03.printDescription();
  }
}
```
则运行结果为：
```
Bike is in gear 1 with a cadence of 20 and travelling at a speed of 10. 

Bike is in gear 5 with a cadence of 20 and travelling at a speed of 10. 
The MountainBike has a Dual suspension.

Bike is in gear 8 with a cadence of 40 and travelling at a speed of 20. 
The RoadBike has 23 MM tires.
```

**如前所述，在Java中，方法调用总是由实际对象的类型决定的，而不是由对象引用的类型决定的。**


**在这个例子中，对象`bike01`, `bike02`, `bike03`所引用的类型都是`Bicycle`类，但他们实际所指的对象类型，则分别是`Bicycle`, `MountainBike`, `RoadBike`。**


可见，虽然我们有多个`printDescription`方法，但Java虚拟机（JVM）会为每个对象调用适当的方法。

是不是还是有点晕乎乎的呢？接下来的讲解会让大家更为明晰。💖

再谈多态
-----
我们前文讲到
```
在Java中，方法调用总是由实际对象指向的类型决定的，而不是由对象引用的类型决定的。

对象bike01, bike02, bike03所引用的类型都是Bicycle类，但他们实际所指的对象类型，则分别是Bicycle, MountainBike, RoadBike。
```
还记得吗？多态指的是一种，为，处在类继承层次结构（也就是一层一层的，从高到低的这种继承关系，一级一级的结构）中的具体对象（一个特定对象，处在类继承层次结构中特定的某一级别、某一层次）选择适当的方法的机制。比如我们在前面的例子中，我们的三个bike对象，分别处在三个不同的层次（一个在父类，两个在子类），然后，我们分别让这三个bike对象，调用了同一个方法名的方法`printDescription`。但是，同一个方法名的方法`printDescription`，实际上有三种不同的形态：`普通自行车(Bicycle)`形态，`山地自行车(MountainBike)`形态，以及`公路自行车(RoadBike)`形态。也就是说，这个`printDescription`方法，是具有多种形态的！`printDescription`这一个被两次重写过的方法，就被称为是多态的方法。

那么，当Java程序在执行时，具体执行`printDescription`这一多态方法的哪一种形态，则取决于，调用这一方法的对象，实际**指向**的对象类型（也就是在`new`语句后紧跟着的类型），而不是这一对象**引用**的对象类型（也就是在`new`语句中，实际对象前面的那个类型
）。例如，在语句
```java
Animal puppy = new Dog();
```
中，实例对象`puppy`所引用的类型是`Animal`，而其实际指向的类型则是`Dog`。

再拿`代欧奇希斯`这只神奇宝贝来作比喻：这是一种长得像外星人的两足神奇宝贝，拥有四种形态，各自注重不同的能力。但，这四种形都态具有共同特征，其躯体都为橘红色，面部都为蓝绿色，背部都有三个蓝绿色的点。
![代欧奇希斯](1.png)


方法的多态性也就像这样，同一个行为具有多个不同表现形式或形态的能力。就如同蝴蝶拥有许多不同的发展形态一样。

让我们回到我们的自行车例子（不要跑偏到神奇宝贝了），来说明多态的存在，所需要的三个前提：

**1. 存在继承关系**

    `MountainBike`类与`RoadBike`类继承了`Bicycle`类。

**2. 子类要重写父类的方法**

    子类重写（Override)了父类的实例方法`printDescription`

**3. 对父类的引用指向子类对象**

测试类`TestBikes`中，语句

```java
Bicycle bike01, bike02, bike03;

bike01 = new Bicycle(20, 10, 1);
bike02 = new MountainBike(20, 10, 5, "Dual");
bike03 = new RoadBike(40, 20, 8, 23);
```
将对于父类`Bicycle`的引用，指向了`Bicycle`, `MountainBike`, `RoadBike`这三个子类对象。



类型转换
-----

在AP CS A中，我们只需要掌握
**向下转型（Downcasting）**
的概念。


考虑如下代码：
```java
//假设getID()方法是GradStudent类中特有的一个public实例方法，没有在Student类中被定义，GradStudent类继承自Student类。
Student student = new GradStudent();
GradStudent gradstudent = new GradStudent();
int x = student.getID(); //编译时错误
int y = gradstudent.getID(); //正确
```

我们可以看到，`student`与`gradstudent`两个实例对象，明明都指向着`GradStudent`这个类，为何
```java
student.getID()
```
会报错呢？

这是因为，尽管实例对象`student`实际指向的是`GradStudent`这个类，但其引用类型仍然为`Student`类，而`Student`类是没有定义一个`getID()`方法的。在编译时，只有`Student`类的非`private`类型的方法，才能使用点号运算符`.`应用于`student`对象。注意，这和我们之前提到的`多态`无关，因为它不满足我们讲过的，`多态`所应该具备的条件：我们没有为子类`GradStudent`重写过getID()方法。因此，这里的`getID()`方法，我们没有赋予它多态性。是故，其只能被用于`GradStudent`类中的实例对象。

那么，如果我们很需要为`student`对象使用`getID()`方法，怎么办呢？

我们可以对`student`对象进行`转型(casting)`，将其强行转为正确的引用类型：
```java
 int x = ((GradStudent) student).getID();
```

因为`student`本已是一个指向`GradStudent`类的对象，只不过其引用对象仍为`Student`，我们的转型可以顺利完成。

像这样的，把一个子类引用指向父类对象的转型过程，称作`向下转型`。

在这个例子中，子类引用就是子类`GradStudent`中的引用方法`getID()`，我们将其强行指向父类对象`student`，使之能够被`student`对象合法地调用。

动态绑定
-----
动态绑定（Dynamic bonding)，指的是，当存在方法重写时，关于调用哪一个实例方法的决定，是在Java程序运行时(run-time)（Java虚拟机JVM实时解析运行Java字节码时）才实时作出的。也就是说，这一个决定是在程序运行时，才实时、动态地作出的。

与之相对的是，当存在方法重载时，关于调用哪一个实例方法的决定，是在Java程序编译时(compile-time)就已经做好的、固化了的，一成不变的的决定，这一种类型被称为静态绑定(Static bonding)。

The compiler selects the correct
overloaded method at compile time by comparing the methods’ signatures. This is
known as static binding, or early binding. In polymorphism, the actual method that
will be called is not determined by the compiler. Think of it this way: The compiler
determines if a method can be called (i.e., is it legal?), while the run-time environment
determines how it will be called (i.e., which overridden form should be used?).
Example 1
Student s = null;
Student u = new UnderGrad("Tim Broder", new int[] {90,90,100},
"none");
Student g = new GradStudent("Kevin Cristella",
new int[] {85,70,90}, "none", 1234);
System.out.print("Enter student status: ");
System.out.println("Grad (G), Undergrad (U), Neither (N)");
String str = IO.readString(); //read user input
if (str.equals("G"))
s = g;
else if (str.equals("U"))
s = u;
else
s = new Student();
s.computeGrade();
Polymorphism 139
When this code fragment is run, the computeGrade method used will depend on the
type of the actual object s refers to, which in turn depends on the user input.
Example 2
public class StudentTest
{
public static void computeAllGrades(Student[] studentList)
{
for (Student s : studentList)
if (s != null)
s.computeGrade();
}
public static void main(String[] args)
{
Student[] stu = new Student[5];
stu[0] = new Student("Brian Lorenzen",
new int[] {90,94,99}, "none");
stu[1] = new UnderGrad("Tim Broder",
new int[] {90,90,100}, "none");
stu[2] = new GradStudent("Kevin Cristella",
new int[] {85,70,90}, "none", 1234);
computeAllGrades(stu);
}
}
Here an array of five Student references is created, all of them initially null. Three of
Polymorphism
applies only to
overridden methods
in subclasses.
these references, stu[0], stu[1], and stu[2], are then assigned to actual objects. The
computeAllGradesmethod steps through the array invoking for each of the objects the
appropriate computeGrademethod, using dynamic binding in each case. The null test
in computeAllGrades is necessary because some of the array references could be null.