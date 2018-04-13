继承
======
继承是Java中非常重要的一个概念。继承反应的是类和类之间的一个关系。还记得在第一章节中，我们提到，类可以具有方法和属性吗？继承，实际上说的就是，"子类"可以继承"父类"的属性，或者是方法。通过继承，可以让信息以一种层级的关系进行管理。

接下来，开始探索继承王国吧！💖

父类和子类的关系
------
一个由其他的类派生出来的类，叫做子类(subclass)，而派生出子类的类，则叫做父类（superclass或parent class)。

在Java中，除了最终超类：Object类，所有的类都有且仅有一个直接的父类（这被称为单继承）。当没有明确在程序中声明某些类所属的父类时，这些类都是最终超类：Object类的（隐式）子类。

类可以层层继承，也就是说，A类可以继承自B类，而B类又继承自C类，C类又有D类派生而来（也就是说，C类又继承自D类），等等等等，子子孙孙无穷尽也。最终，就如同基因学上，所有的人类都来自于"Y染色体亚当"和"X染色体夏娃"一样，层层推溯以后，所有的类都最终派生于一个"终极(topmost)"类，也就是最终超类：Object类。我们可以用树的枝桠来形容，这棵树，我们叫它"继承树"。Object类，作为最终超类，就是这棵树最底层的那个"万物之源"。

继承的概念是简单而强大的。当你想创建一个新的类，而此时已经有既成的一个类包含了你想要的一些信息（也就是描述方法或属性的代码），你就可以直接在已经存在的类的基础上，派生出一个新的类，让那个派生出来的新类，来继承旧类的属性和方法。在这样的过程中，我们可以避免重复编写与调试已经写过的类中的代码，也就是程序员常说的"避免重复造轮子"。

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

// 狗
class Dog extends Mammal{
}
```
```java
public class Bicycle {

    // the Bicycle class has three fields
    public int cadence;
    public int gear;
    public int speed;

    // the Bicycle class has one constructor
    public Bicycle(int startCadence, int startSpeed, int startGear) {
        gear = startGear;
        cadence = startCadence;
        speed = startSpeed;
    }

    // the Bicycle class has four methods
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
```Java
public class MountainBike extends Bicycle {

    // the MountainBike subclass adds one field
    public int seatHeight;

    // the MountainBike subclass has one constructor
    public MountainBike(int startHeight,
                        int startCadence,
                        int startSpeed,
                        int startGear) {
        super(startCadence, startSpeed, startGear);
        seatHeight = startHeight;
    }   

    // the MountainBike subclass adds one method
    public void setHeight(int newValue) {
        seatHeight = newValue;
    }   
}
```
下面是练习框，让我们跟着练习框的下方的指示一起来熟悉一下练习环境吧。

<lab lang="blocks" parameters="logic=false&math=false&loops=false&lists=false&color=false&variables=false&functions=false&text=false&name=chapter1lab1">
  <notice>练习环境在此无法显示，请移步至[程谱 coderecipe.cn](https://coderecipe.cn/learn/1)查看。</notice>
</lab>

首先，点击左边的“输入输出”，将“输出”块拖到右边。然后，修改一下文字“abc”成“Hello World!”，再点击右边的红色按钮运行。
结果应该是这样：
![运行截图](Pic2.png)

那输入呢？ 让我们把“输入文字并提示消息”块插到“输出”块上，这里的提示消息指的是在输入文字的时候会告诉我们程序的使用者输入的文字的含义，同样点击运行，首先输入一些文字，然后点确认，这串文字就会被输出了。当然，我们也可以通过下拉框选择让这个输入块读取数字，试一试吧。

如果想删除一个块，把它拖到右下角的垃圾桶图标上就好了。

![运行截图](Pic3.png)

细心的你可能会发现，在选择输入数字以后，如果输入的不是一个数字，就会输出NaN，这是为什么呢？其实NaN的意思是Not a Number，代表程序告诉我们输入的并不是一个数字。

这样，我们就做出了一个小程序，它能读取用户的输入，然后对数字进行处理，然后输出回来，是不是很有意思呀~

计算
------
刚才我们学完了最基本的输入输出，那接下来我们可以更进一步，学一下如何让计算机来为我们进行运算。

<lab lang="blocks" parameters="logic=false&loops=false&lists=false&color=false&variables=false&functions=false&text=false&name=chapter1lab2">
  <notice>练习环境在此无法显示，请移步至[程谱 coderecipe.cn](https://coderecipe.cn/learn/1)查看。</notice>
</lab>

你可能会发现，这个练习环境和之前不一样，因为这里多了一个“数学”按钮，点进去以后会发现里面全都是数学运算，看起来好复杂的样子。让我们从简单的开始，先拖动一个“1+1”块（其实这是四则运算加乘方块，我们等一会儿就知道啦），插在“输出”块上，点击运行，大功告成啦！
![运行截图](Pic4.png)

这个“1+1”块可没有看起来那么简单，这个块是可是可以高度定制的呢！我们可以1+1成为任意的四则运算内容，比如10÷5。而且这个“1+1”块内部还可以嵌入其他块，这样就可以做好多次加减乘除啦。

我们还可以把输入块放入这个运算块里，不过记得选择“输入数字并显示消息”而不是“输入文字并显示消息”，不然是放不进运算块的，毕竟文字可不能进行四则运算。

像底下这样组合块就可以做出一个除法计算器啦！
![运行截图](Pic5.png)

小练习
------
让我们来练习一下我们刚学习的知识吧。
<lab lang="blocks" parameters="logic=false&loops=false&lists=false&color=false&variables=false&functions=false&text=false&name=chapter1lab3">
  <notice>练习环境在此无法显示，请移步至[程谱 coderecipe.cn](https://coderecipe.cn/learn/1)查看。</notice>
</lab>

试试做出如下的效果：

1. 输出“我要认真学习编程” （不带引号）
2. 计算1000-985并输出
3. 计算(100-58)\*2并输出
4. 把输入的数值加上10输出
5. 把输入的数值平方（也就是四则运算加乘方块里面的^2）输出

学到这里，你就已经算是入门计算机编程啦👏，加油加油继续学习吧~
