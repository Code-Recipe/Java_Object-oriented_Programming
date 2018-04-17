<notice>教程读者请不要直接阅读本文件，因为诸多功能在此无法正常使用，请移步至[程谱 coderecipe.cn](https://coderecipe.cn/learn/1)学习完整教程。如果您喜欢我们的教程，请在右上角给我们一个“Star”，谢谢您的支持！</notice>

引用
======

接下来让我们一起看看引用这一章吧😃

原始类型和引用类型
-----
在Java里面的类型有分两种，**原始类型**（primitive types）和**引用类型**（reference types）。Java自带的类型中，凡是首字母为小写的都是原始类型（如`int`，`bool`，`double`），凡是首字母为大写的都是引用类型（如`String`，`Object`），自己定义的类的类型（比如之前说的`Car`）也都是引用类型。

那么这两种类型有什么区别呢？主要的区别在于储存方式。原始类型的数据是直接储存的，这在Java入门教程的[变量和类型](https://coderecipe.cn/learn/2?chapter=2)一章中有详细描述不同变量在Java中的表示和储存方式。而引用类型是按引用（reference）储存，就是变量**只是记下了这个对象真正的位置**，而**并不是储存了整个对象**。接下来让我们用两个例子来重点区分一下这两种储存方式。

首先我们拿原始类型`int`来做个实验：

<lab lang="java" parameters="filename=Hello.java">
<notice>练习环境在此无法显示，请移步至[程谱 coderecipe.cn](https://coderecipe.cn/learn/2)查看。</notice>
public class Hello {
  public static void main(String[] args) {
      int a = 1;
      int b = a;
      b = 2;
      System.out.println(a);
      System.out.println(b);
  }
}
</lab>

这段代码输出1和2，正如我们所料，因为`a`被赋值为1以后我们又把`a`的值给了`b`，也就等价于`b = 1`，最后我们再把2赋值给`b`就和`a`没关系了。

让我们再看看这个简写过的`Dog`类改编的小实验：

<lab lang="java" parameters="filename=Dog.java">
<notice>练习环境在此无法显示，请移步至[程谱 coderecipe.cn](https://coderecipe.cn/learn/1)查看。</notice>
public class Dog {
  int age;
  public void showInfo(){
    System.out.println("I'm " + age + " years old.");
  }
  public static void main(String[] args) {
    Dog myPuppy = new Dog();
    myPuppy.age = 2;
    Dog mySecondPuppy = myPuppy;
    mySecondPuppy.age = 3;
    myPuppy.showInfo();
    mySecondPuppy.showInfo();
  }
}
</lab>

我们还是一样给我们的变量赋值，然而这次两个`showInfo`输出的都是`I'm 3 years old.`。这是因为`Dog`是我们定义的类，也就是一个引用类型，那么储存方式也自然是按引用来进行，`myPuppy`这个变量并不储存整个对象，而是指向了在`new`运算符被执行到时生成的对象（相当于把那个真正的对象的位置储存了下来），因此当我们把`myPuppy`赋值给`mySecondPuppy`的时候，我们只是把那个对象的位置给了`mySecondPuppy`，并没有生成新的对象，在这整段代码中，只有一个`Dog`对象真正被产生（只有一个`new`被执行），其他都只是位置的传递。而在实际操作的时候，我们又通过`mySecondPuppy`操作了那个对象的`age`属性，而`myPuppy.showInfo()`又读取了那个对象的`age`属性，因此会读到我们修改后的3而不是2。


空引用
-----
在上一节我们说到，一个`new`操作符生成一个真的对象。那么如果我们在定义的时候没有初始化（也就是没有用`new`操作符新建对象）会怎样呢？

<lab lang="java" parameters="filename=Dog.java">
<notice>练习环境在此无法显示，请移步至[程谱 coderecipe.cn](https://coderecipe.cn/learn/1)查看。</notice>
public class Dog {
  int age;
  public void showInfo(){
    System.out.println("I'm " + age + " years old.");
  }
  public static void main(String[] args) {
    Dog myPuppy;
  }
}
</lab>

那让我们试着调用一下它的方法：

<lab lang="java" parameters="filename=Dog.java">
<notice>练习环境在此无法显示，请移步至[程谱 coderecipe.cn](https://coderecipe.cn/learn/1)查看。</notice>
public class Dog {
  int age;
  public void showInfo(){
    System.out.println("I'm " + age + " years old.");
  }
  public static void main(String[] args) {
    Dog myPuppy;
    myPuppy.showInfo();
  }
}
</lab>

这时候Java会提示`variable myPuppy might not have been initialized`，这是因为Java注意到我们没有**初始化**（initialize）这个变量，也就是没给它赋值就调用，不让我们编译通过，因为这显然是会造成问题的。

上面说的是我们在一个方法里定义`myPuppy`的情况，但如果在一个类里定义`myPuppy`，情况则完全不同，例如每一个`Dog`对象都会有一个`son`属性，这个`son`直接定义在类的内部，如下所示：

<lab lang="java" parameters="filename=Dog.java">
<notice>练习环境在此无法显示，请移步至[程谱 coderecipe.cn](https://coderecipe.cn/learn/1)查看。</notice>
public class Dog {
  int age;
  Dog son;
  public void showInfo(){
    System.out.println("I'm " + age + " years old.");
  }
  public static void main(String[] args) {
    Dog myPuppy = new Dog();
    System.out.println(myPuppy.son);
    myPuppy.son.showInfo();
  }
}
</lab>

运行代码以后会发现，我们的程序先输出了`null`，又抛出了一个异常`Exception in thread "main" java.lang.NullPointerException`（还记得我们在Java入门教程里说过的异常是在运行的时候而不是在编译的时候抛出的吗）。**这是因为如果我们在类的实例里面（而不是方法里面）定义了却没有初始化一个变量，Java会给这个变量`null`值**，这个带有`null`值的引用叫做空引用，这个异常说的是我们在试图访问一个值为`null`的变量的方法或者属性。在程序运行的时候，如果遇到了这个错误，那么可能是前面的哪一步出错了，导致程序所读取的对象的值是`null`。

运行的时候抛出`java.lang.NullPointerException`固然很吓人，除了用`catch`来接住这个异常以外，我们还可以在异常发生前通过判断是不是`null`来避免使用到值为`null`的变量：

<lab lang="java" parameters="filename=Dog.java">
<notice>练习环境在此无法显示，请移步至[程谱 coderecipe.cn](https://coderecipe.cn/learn/1)查看。</notice>
public class Dog {
  int age;
  public void showInfo(){
    System.out.println("I'm " + age + " years old.");
  }
  public static void main(String[] args) {
    Dog myPuppy = null;
    if(myPuppy != null) {
      myPuppy.showInfo();
    } else {
      System.out.println("myPuppy is null");
    }
  }
}
</lab>

通过判断`myPuppy`这个变量是不是异常然后分别采取操作，我们成功避免了`java.lang.NullPointerException`这个异常。

小练习
-----

在这里练习吧：
<lab lang="java" parameters="filename=Hello.java">
<notice>练习环境在此无法显示，请移步至[程谱 coderecipe.cn](https://coderecipe.cn/learn/1)查看。</notice>
public class Hello {
   public static void main(String[] args) {
     // 在这里添加你的代码
   }
}
</lab>