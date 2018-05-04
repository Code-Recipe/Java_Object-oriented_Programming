一个特殊而又重要的类——String类
=====
**Java面向对象的最后一章啦！再接再厉！**

`String`是Java中特殊的一种类，它是一种引用类型，而不是原始数据类型（注意`String`类是大写字母开头的）。`String`类型的对象是字符串，也就是一系列的字符。所有`String`类型的变量, 例如```Hello World!```，都作为实例变量成为类的一个实例对象，这样的变量，称作**字面量(literal)**。一个`String`类型的字面量，包含着零个（包括0）以上的字符，字符的涵义包括双引号`" "`中的所有字符，包括空格与转义符。（双引号本身不属于字面量的一部分）。如下几个例子都是合法的字面量。
```
"" //这是一个空的字面量
```

```
"2468"
```

```
"I must\n go home"
```
`String`类型的对象（字面量）是不可变的，也就是说，一旦被初始化赋值以后，这个字面量的内容就与字面量的对象名绑定了，后期没有任何方法可以进行更改。例如，我们用语句
```java
String s = "Hello World!"
```
为`s`赋值后，`s`的内容在后期就不可能被改动了。

但是，你可以创建新的`String`类型对象（新的字面量）来作为现有的字面量的衍生变化（更新）。

String对象的创建和更新
-----
`String`类的对象（字面量）特殊在于，它们可以像一个原始数据类型的对象一样被初始化，例如
```java
String s = "Hello World!";
```
就创建了一个值为`Hello World!`（注意不包括双引号）的字面量`s`。
我们也可以使用的一般的为类创建实例对象的语句，二者是等价的：
```java
String s = new String("Hello World!");
```
在上述两个语句例子中，`s`都是一个值为`Hello World!`的字面量。

我们可以**更新**一个`String`类型的字面量：
```java
String s = "Sam";
s = "Tony";
```
这相当于
```java
String s = new String("Sam");
s = new String("Tony");
```
同学们可能会感到疑惑：我们前面不是说了，字面量一旦定义，就不可**改变**吗？其实，这并不矛盾。我们第一次定义的`John`并没有被**改变**，它只是被直接弃置了。相当于说，`s`对象原本指向内存中一块存储着`John`这个值的地址，后来，对这个地址的指向直接被弃置了，`s`对象被重新定向到内存中一块存储着`Harry`这个值的地址。也就是说，这个字面量是被**更新**了。

同样的，我们也可以这样更新`s`字面量：
```java
s = "Hello"
s = s + " Tony!";
```
s的字面量最终被更新为`Hello Tony!`

例如，我们有两个对象`lhs`和`rhs`，则语句`lhs + rhs`将生成一个新的字符串，内容为`lhs`的值紧紧跟随者`rhs`的值。如果`lhs`和`rhs`本身都不是`String`类型的字面量，则Java会自动为`lhs`和`rhs`对象调用`toString()`方法，然后将`toString()`方法返回的`String`类型的值串联在一起。（是的，如果我们没有为`lhs`与`rhs`对象重写`toString()`方法，最后得到的值可能会很奇怪，不是我们想要的。）如果，其中一个对象是`String`类型，而另一个对象是原始数据类型中的一种，则那个原始数据类型的对象会自动被转为`String`类型的对象，然后再进行串联。如果两个对象都不是`String`类型的对象，则会报错。

这个例子中的代码可以工作：
<lab lang="java" parameters="filename=Hello.java">
<notice>练习环境在此无法显示，请移步至[程谱 coderecipe.cn](https://coderecipe.cn/learn/3)查看。</notice>
public class Hello {
   public static void main(String[] args) {
       int number = 7;
       String sayNumber = "The number is ";
       sayNumber = sayNumber + number;
       System.out.println(sayNumber);
   }
}
</lab>
最终串联起了字符串。

而下面这段代码无法运行：

```java
int x = 3, y = 4;
String sum = x + y;
```
则会报错。我们不能把`int`类型的值直接赋给`String`类型的sum，因为语句x+y中，+运算符的操作对象是两个`int`型对象，其都不是`String`类型对象。在这里，`+`进行代数加法运算，而非字符串串联运算。


假设我们为一个类重写了`toString()`方法，使之能够返回一个`String`类型的日期，例如
```
14/4/2018.
```
这个类定义两个对象`d1`与`d2`如下：
```java
Date d1 = new Date(14, 4, 2018);
Date d2 = new Date(26, 7, 2017);
```
则
```java
String s = "My birthday is " + d2;
```
将会返回
```
My birthday is 26/7/2017
```
而
```java
String s2 = d1 + d2; //error: + not defined for objects
```
将会出现错误。
而
```java
String s3 = d1.toString() + d2.toString();
```
将会返回
14/4/201826/7/2017


String类的方法
-----
在AP中，我们需要了解`String`类的几个内置方法：
### 1.length()方法
用法:
```java
int length()
```
以`int`型返回字符串的长度。

### 2.substring(int startIndex)方法
用法:
```java
String substring(int startIndex)
```
该方法返回一个新的字符串，作为原字符串的子字符串。该字符串将传入的参数（必须为非负整数）开始作为起始位置，以字符串最后一个字符作为截止位置，来截取原字符串的一段，作为新的字符串。注意，`startIndex`是从零开始数的！所以下面这个例子中，`startIndex`是4而不是5。
看这个例子：
```java
public class Test {
    public static void main(String args[]) {
        String Str = new String("www.coderecipe.cn");
        System.out.print("返回值 :" );
        System.out.println(Str.substring(4) );
    }
}
```
返回值为
```java
coderecipe.cn

```
注意，如果传入参数`startIndex`的值为负数或大于字符串的长度，将抛出
```java
IndexOutOfBoundsException
```

### 3.substring(int startIndex, int endIndex)方法
用法：
```java
String substring(int startIndex, int endIndex)
```
和上面的`substring(int startIndex)`方法一样，该方法也是返回一个新的字符串，作为原字符串的子字符串。只不过在这个方法中，我们规定了截取原字符串的终止位置。注意：`startIndex`（起始索引）是包括的，而`endIndex`（截止索引）是不包括的，也就是说，`startIndex`是你要的第一个字符，而`endIndex`是你不想要的第一个字符。例如：
```java
public class Test {
    public static void main(String args[]) {
        String Str = new String("www.coderecipe.cn");
        System.out.print("返回值 :" );
        System.out.println(Str.substring(4,14) );
    }
}
```
返回值为
```java
coderecipe
```

### 4.indexOf(String str)方法
用法：
```java
int indexOf(String str)
```
该方法的作用是，返回一个子字符串的第一个字符在原字符串中的位置。
例如：
```java
String s = "funnyfarm";
int x = s.indexOf("farm"); //x has value 5
```
注意，这里的返回值是5而不是6，也就是说，因为这也是从0开始计数的。
如果一个字符串不是另一个字符串的子字符串，就会返回`-1`，例如：
```java
String s = "funnyfarm";
int x = s.indexOf("farmer"); //x has value -1
```
如果一个字符串是空的，而我们用`indexOf()`去试图找出这个空字符串在原字符串中的索引，则会抛出`NullPointerException`错误。

String类的比较
-----
有两种比较字符串对象的方法：
1.使用从`Object`类继承并重写的`equals`方法：
```java
if (string1.equals(string2)) ...
```
如果string1和string2是相同的字符串，则返回true，否则返回false。

2. 使用`compareTo()`方法。用法：
```java
`int compareTo(String otherString)`
```
该方法用于按字典顺序比较两个字符串。

该方法返回值是整型,它是先比较对应字符的大小(ASCII码顺序),如果第一个字符和参数的第一个字符不等,结束比较,返回他们之间的差值,如果第一个字符和参数的第一个字符相等,则以第二个字符和参数的第二个字符做比较,以此类推,直至比较的字符或被比较的字符有一方：

如果参数字符串等于此字符串，则返回值 0；
如果此字符串小于字符串参数，则返回一个小于 0 的值；
如果此字符串大于字符串参数，则返回一个大于 0 的值。

例如：
```java
public class Test {

    public static void main(String args[]) {
        String str1 = "Strings";
        String str2 = "Strings";
        String str3 = "Strings123";

        int result = str1.compareTo( str2 );
        System.out.println(result);

        result = str2.compareTo( str3 );
        System.out.println(result);

        result = str3.compareTo( str1 );
        System.out.println(result);
    }
}
```
的结果为
```
0
-3
3
```
字符根据它们在ASCII图表中的位置进行比较。 你所有需要知道的是，所有数字都在所有大写字母之前，所有大写字母都在小写字母之前。 因此，“5”出现在“R”之前，"R"出现在"a"之前。 比较两个字符串的时候，从每个字符串的左端开始，逐字符比较，直到到达两个字符串开始出现差异第一个字符，例如第k个字符。 如果`s1`的第k个字符在`s2`的第k个字符之前，那么`s1`将在`s2`之前，反之亦然。 如果两个字符串`s1`和`s2`同一个位置的每个字符都相等，但`s1`比`s2`短（相当于`s1`是`s2`的非空真子集），则`s1`在`s2`之前。
例如：
```java
String s1 = "HOT", s2 = "HOTEL", s3 = "dog";
if (s1.compareTo(s2) < 0)) //true, s1 terminates first
...
if (s1.compareTo(s3) > 0)) //false, "H" comes before "d"
```

### **注意：不要使用`==`运算符来比较字符串！**
语句
```java
if(string1 == string2)
```
测试`string1`与`string2`是否指向同一个引用对象。但这并不测试两个字符串是否拥有相同的内容。 例如：
```java
String s = "oh no!";
String t = "oh no!";
if (s == t) ...
```
这么做返回的值是`true`，尽管`s`和`t`**看起来**不是同一个引用对象。 原因是为了提高效率，Java只为等价的字符串文字创建了一个String对象，而不是两个。因此`s`与`t`实际上指向同一个对象。这是安全的，因为字符串不能被改变。

再看下面这个例子：
```java
String s = "oh no!";
String t = new String("oh no!");
if (s == t) ...
```
这个测试的结果是`false`，因为我们强心创建了一个新的引用对象。`s`和`t`在此时就不指向同一个引用对象了。

这个故事的寓意是什么？ 在于，我们应该总是使用`equals()`方法而非`==`来测试字符串。`equals()`方法总是做正确的事情。


小练习
-----
1.Refer to these declarations:

```java
Integer k = new Integer(8);
Integer m = new Integer(4);
```

Which test will not generate an error?

I if (k.intValue() == m.intValue())...

II if ((k.intValue()).equals(m.intValue()))...

III if ((k.toString()).equals(m.toString()))...

(A) I only

(B) II only

(C) III only

(D) I and III only

(E) I, II, and III

<cr type="hidden"><notice>隐藏内容功能在此无法正常显示，请移步至[程谱 coderecipe.cn](https://coderecipe.cn/learn/3)查看。</notice>B</cr>

2.【2015年AP CS第11题】Consider the following method.

```java
public static boolean mystery(String str)
{
String temp = "";
for (int k = str.length(); k > 0; k--)
{
temp = temp + str.substring(k - 1, k);
}
return temp.equals(str);
}
```

Which of the following calls to mystery will return true?

(A) mystery("no")

(B) mystery("on")

(C) mystery("nnoo")

(D) mystery("nono")

(E) mystery("noon")

<cr type="hidden"><notice>隐藏内容功能在此无法正常显示，请移步至[程谱 coderecipe.cn](https://coderecipe.cn/learn/3)查看。</notice>E</cr>


3.Consider the following recursive method.

```java
public static void whatsltDo(String str)
{
int len = str.length(); 

if (len > 1)
  {
   String temp = str.substring(0, len - 1); 
   System.out.printIn(temp); 
   whatsltDo(temp);
  }
}
```

What is printed as a result of the call whatsltDo ("WATCH") ?

(A) H

(B) WATC

(C) ATCH

  ATC

  AT

  A

(D) WATC

  WAT

  WA

  W

(E) WATCH

  WATC 

  WAT
     
  WA

<cr type="hidden"><notice>隐藏内容功能在此无法正常显示，请移步至[程谱 coderecipe.cn](https://coderecipe.cn/learn/3)查看。</notice>D</cr>

4.Consider the following method.

```java
public String mystery(String input)
{
  String output = "";

  for (int k = 1; k < input.length(); k = k + 2)
  {
    output += input.substring(k, k + 1);
  }

  return output;
}
```

What is returned as a result of the call mystery ("computer") ?

(A) "computer"

(B) "cmue"

(C) "optr"

(D) "ompute"

(E) Nothing is returned because an IndexOutOfBoundsException is thrown.

<cr type="hidden"><notice>隐藏内容功能在此无法正常显示，请移步至[程谱 coderecipe.cn](https://coderecipe.cn/learn/3)查看。</notice>C</cr>

### 实验室

在这里练习吧：
<lab lang="java" parameters="filename=Hello.java">
<notice>练习环境在此无法显示，请移步至[程谱 coderecipe.cn](https://coderecipe.cn/learn/3)查看。</notice>
public class Hello {
   public static void main(String[] args) {
     // 在这里添加你的代码
   }
}
</lab>
