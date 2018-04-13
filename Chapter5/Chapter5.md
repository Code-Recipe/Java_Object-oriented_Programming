多态
======
初识多态
-----
多态(Polymorphism)也是Java面向对象编程中非常重要的一个概念。多态，原本指的是在生物学中，一个生物体或物种，可以有不同的形态或发育阶段（例如蝴蝶的变态）。在Java中，多态指的是，同一个行为具有多个不同表现形式或形态的能力。多态的好处是，可以使程序有良好的扩展，并可以对所有类的对象进行通用处理。

多态的概念，与前一节我们讲过的`方法重写`有着紧密的关联。一个至少在一个子类中被重写过的方法，就被称为是多态的方法。

对于被重写过的方法，它们都具有相同的方法名。那么Java在运行的时候，该如何是好？Java是依靠什么机制，来选择具体要执行哪一个方法的呢？

**在Java中，方法调用总是由实际对象的类型决定的，而不是由对象引用的类型决定的。**

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
在Java中，方法调用总是由实际对象的类型决定的，而不是由对象引用的类型决定的。

对象bike01, bike02, bike03所引用的类型都是Bicycle类，但他们实际所指的对象类型，则分别是Bicycle, MountainBike, RoadBike。
```
注意，多态是
