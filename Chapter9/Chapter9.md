程序分析与设计
=====
终于！到最后一章啦！再接再厉吧！在AP考试中，这一章节的内容以理解为主，有点像文科内容，大家加油！

瀑布模型(The waterfall Model)
-----
设计一个成功的程序需要大量的步骤，而瀑布模型就是一种很有逻辑性的程序设计过程。

瀑布模型核心思想是按流程将问题化简，将功能的实现与设计分开，便于分工协作，即采用结构化的分析与设计方法将逻辑实现与物理实现分开。将软件生命周期划分为制定计划和需求分析、软件设计、程序编写、软件测试和运行维护等五个基本活动，并且规定了它们自上而下、相互衔接的固定次序，如同瀑布流水，逐级下落。

### 1. 程序需求分析

程序需求分析是设计一个程序的第一步，在设计一个程序前，我们要知道我们想让程序干什么。一般是根据顾客的需求进行设计我们的程序，对于程序的需求进行分析，确保顾客想要的能够实现，并且程序员将顾客所没提及到的一些事情进行阐述说明。确保最后做出来的是顾客想要的。


### 2. 程序设计
对于小型程序我们可以进行直接编写。但是作为一个优秀的程序员，需要有一个对于自己程序的一个具体计划：这个程序有什么，能干什么，需要几个模块，诸如此类。


### 3. 程序编写
程序编写要根据语言进行区分，在我们设计程序的时候就应该确定了是面向对象还是面向过程。在AP中，我们选择的是Java语言。要根据Java语言的一些特性编写我们的程序。

### 4.调试和测试
#### i. 数据测试
我们在调试数据的时候，我们要把数据类型和可能的值都要考虑进去，以防止出现出乎意料的bugs。事实上，产品使用者能干出的事情是丧心病狂的，所以我们在推出产品前一定要对数据类型进行全方面测试。同时，这也涉及到了程序稳健性(robustness)问题。我们不能够允许程序给出错误答案，不能够允许在数据类型错误的时候程序崩溃，不能允许对于错误类型数据程序照样执行。

例如，对于一个排列函数，参数为`int`类型。这个函数是为了将数据插入到现有数组中，并且排列顺序正确。
已知数组：2，5，233。测试值就需要包括：比2小的；2到5之间的；5到233之间的；233以上的；2,5,233这三个数；负数。

#### ii.bug类型
**编译错误(compile-time error)**
指的是在编译时的错误。比如语言使用错误，调用错误，缺少符号等。

**运行错误(run-time error)**
是指编译时未报错，但是运行时出现的错误。比如子类函数在调用父类函数时出现的问题，数据中分母为0，无限循环.在Java中，这些错误都会以Exception的方式抛出(throws)。

**逻辑错误(intent or logic error)**
是并没有明显提示，程序可以正常运行。但结果并不是我们想要的。

#### 5. 程序维护(maintenance)

维护数据，更新方法，增加新特性，等等。



面向对象程序设计
-----
### 1.面向对象程序设计步骤
面向对象程序设计需要有几个步骤：

1. 确定类
2. 确定行为
3. 确定类之间的关系
4. 继承关系(is-a的关系)
5. 组合关系(has-a的关系，AP中并未涉及)

### 2.UML图
绘制UML图是一个程序员的好习惯。但因为这并不是AP Java中的考点，这里并不深入的去讲解。有兴趣的同学可以进行展开了解。

### 3.程序开发
1. 自下而上开发(bottom-up)：写多个零散的代码块，再逐渐组合连接关系。
2. 自上而下开发(top-down)：写出主体块，再分解为多个零散的代码。

### 4.方法书写
方法书写的具体讲解在前面的章节有提到。对于属性的隐藏(private来修饰属性)也有提到。在书写方法的时候，我们为了节约CPU的占用率以及迅速得出结果我们在书写部分方法时要采用一些算法(algorithm)来帮助我们。一些好算法可以节约CPU运算时间以及节约我们的内存，这些算法就是高效算法。但是对于算法的使用实际上还存在一定范围的争辩。采不采用算法完全取决于程序员本身。

### 5.确定类
关于类名的确认一定要简洁直接，但是要避免几种类别的命名，大家领会一下意思:

Program (永远不要用program来命名，完全不清楚是用来干什么的)

Teacher（男和女有时候有不同的名字，性别错了有些尴尬）

Data，Record（跟方法名字可能重合，避免混淆）

Class(和class关键字重名，不要使用)