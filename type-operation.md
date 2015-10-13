# 基本类型与运算符

# Java 基本数据类型

java 基本类型
作者：臧圩人

基本类型，或者叫做内置类型，是 JAVA 中不同于类的特殊类型。它们是我们编程中使用最频繁的类型，因此面试题中也总少不了它们的身影，在这篇文章中我们将从面试中常考的几个方面来回顾一下与基本类型相关的知识。

基本类型共有八种，它们分别都有相对应的包装类。关于它们的详细信息请看下表：

基本类型可以分为三类，字符类型 char，布尔类型 boolean 以及数值类型 byte、short、int、long、float、double。数值类型又可以分为整数类型 byte、short、int、long 和浮点数类型 float、double。JAVA 中的数值类型不存在无符号的，它们的取值范围是固定的，不会随着机器硬件环境或者操作系统的改变而改变。实际上，JAVA 中还存在另外一种基本类型 void，它也有对应的包装类 java.lang.Void，不过我们无法直接对它们进行操作。对于数值类型的基本类型的取值范围，我们无需强制去记忆，因为它们的值都已经以常量的形式定义在对应的包装类中了。请看下面的例子：

Java代码

```
public class PrimitiveTypeTest {  
    public static void main(String[] args) {  
        // byte  
        System.out.println("基本类型：byte 二进制位数：" + Byte.SIZE);  
        System.out.println("包装类：java.lang.Byte");  
        System.out.println("最小值：Byte.MIN_VALUE=" + Byte.MIN_VALUE);  
        System.out.println("最大值：Byte.MAX_VALUE=" + Byte.MAX_VALUE);  
        System.out.println();  
  
        // short  
        System.out.println("基本类型：short 二进制位数：" + Short.SIZE);  
        System.out.println("包装类：java.lang.Short");  
        System.out.println("最小值：Short.MIN_VALUE=" + Short.MIN_VALUE);  
        System.out.println("最大值：Short.MAX_VALUE=" + Short.MAX_VALUE);  
        System.out.println();  
  
        // int  
        System.out.println("基本类型：int 二进制位数：" + Integer.SIZE);  
        System.out.println("包装类：java.lang.Integer");  
        System.out.println("最小值：Integer.MIN_VALUE=" + Integer.MIN_VALUE);  
        System.out.println("最大值：Integer.MAX_VALUE=" + Integer.MAX_VALUE);  
        System.out.println();  
  
        // long  
        System.out.println("基本类型：long 二进制位数：" + Long.SIZE);  
        System.out.println("包装类：java.lang.Long");  
        System.out.println("最小值：Long.MIN_VALUE=" + Long.MIN_VALUE);  
        System.out.println("最大值：Long.MAX_VALUE=" + Long.MAX_VALUE);  
        System.out.println();  
  
        // float  
        System.out.println("基本类型：float 二进制位数：" + Float.SIZE);  
        System.out.println("包装类：java.lang.Float");  
        System.out.println("最小值：Float.MIN_VALUE=" + Float.MIN_VALUE);  
        System.out.println("最大值：Float.MAX_VALUE=" + Float.MAX_VALUE);  
        System.out.println();  
  
        // double  
        System.out.println("基本类型：double 二进制位数：" + Double.SIZE);  
        System.out.println("包装类：java.lang.Double");  
        System.out.println("最小值：Double.MIN_VALUE=" + Double.MIN_VALUE);  
        System.out.println("最大值：Double.MAX_VALUE=" + Double.MAX_VALUE);  
        System.out.println();  
  
        // char  
        System.out.println("基本类型：char 二进制位数：" + Character.SIZE);  
        System.out.println("包装类：java.lang.Character");  
        // 以数值形式而不是字符形式将Character.MIN_VALUE输出到控制台  
        System.out.println("最小值：Character.MIN_VALUE="  
                + (int) Character.MIN_VALUE);  
        // 以数值形式而不是字符形式将Character.MAX_VALUE输出到控制台  
        System.out.println("最大值：Character.MAX_VALUE="  
                + (int) Character.MAX_VALUE);  
    }  
}  
```

运行结果：

1、基本类型：byte 二进制位数：8
2、包装类：java.lang.Byte
3、最小值：Byte.MIN_VALUE=-128
4、最大值：Byte.MAX_VALUE=127
5、
6、基本类型：short 二进制位数：16
7、包装类：java.lang.Short
8、最小值：Short.MIN_VALUE=-32768
9、最大值：Short.MAX_VALUE=32767
10、
11、基本类型：int 二进制位数：32
12、包装类：java.lang.Integer
13、最小值：Integer.MIN_VALUE=-2147483648
14、最大值：Integer.MAX_VALUE=2147483647
15、
16、基本类型：long 二进制位数：64
17、包装类：java.lang.Long
18、最小值：Long.MIN_VALUE=-9223372036854775808
19、最大值：Long.MAX_VALUE=9223372036854775807
20、
21、基本类型：float 二进制位数：32
22、包装类：java.lang.Float
23、最小值：Float.MIN_VALUE=1.4E-45
24、最大值：Float.MAX_VALUE=3.4028235E38
25、
26、基本类型：double 二进制位数：64
27、包装类：java.lang.Double
28、最小值：Double.MIN_VALUE=4.9E-324
29、最大值：Double.MAX_VALUE=1.7976931348623157E308
30、
31、基本类型：char 二进制位数：16
32、包装类：java.lang.Character
33、最小值：Character.MIN_VALUE=0
34、最大值：Character.MAX_VALUE=65535

Float 和 Double 的最小值和最大值都是以科学记数法的形式输出的，结尾的“E+数字”表示 E 之前的数字要乘以10的多少倍。比如3.14E3就是3.14×1000=3140，3.14E-3就是3.14/1000=0.00314。

大家将运行结果与上表信息仔细比较就会发现 float、double 两种类型的最小值与Float.MIN_VALUE、 Double.MIN_VALUE 的值并不相同，这是为什么呢？实际上Float.MIN_VALUE 和 Double.MIN_VALUE 分别指的是 float 和 double 类型所能表示的最小正数。也就是说存在这样一种情况，0到 ±Float.MIN_VALUE 之间的值 float 类型无法表示，0 到 ±Double.MIN_VALUE 之间的值 double 类型无法表示。这并没有什么好奇怪的，因为这些范围内的数值超出了它们的精度范围。

基本类型存储在栈中，因此它们的存取速度要快于存储在堆中的对应包装类的实例对象。从 Java5.0（1.5）开始，JAVA 虚拟机（Java Virtual Machine）可以完成基本类型和它们对应包装类之间的自动转换。因此我们在赋值、参数传递以及数学运算的时候像使用基本类型一样使用它们的包装类，但这并不意味着你可以通过基本类型调用它们的包装类才具有的方法。另外，所有基本类型（包括 void）的包装类都使用了 final 修饰，因此我们无法继承它们扩展新的类，也无法重写它们的任何方法。

# JAVA 基础之 java 运算符大百科

运算符用于执行程序代码运算，会针对一个以上操作数项目来进行运算。下面介绍 JAVA 中的运算符。
    
**一、算术运算符：**
单目：+（取正）-（取负） ++（自增1） - -（自减1） 双目：+ - * / %（取余） 三目：a>b?true:false 说明：当 a 大于 b 的时候，为 true（也就是冒号之前的值），否则为false;这整个运算符包括一个关系运算符（可以是">""<""!="等等），一个"?",一个":",冒号前后需要有两个表达式或者是值或者是对象。
    
**二、关系运算：**
等于符号：==,不等于符号： != ,大于符号：>, 小于符号：<,大于等于符号： >= ,小于等于符号： <= .
    
**三、位运算符 逻辑运算符：**
位运算符 与（&）、非（~）、或（|）、异或（^）&:当两边操作数的位同时为1时，结果为1,否则为0.如1100&1010=1000 | :当两边操作数的位有一边为1时，结果为0,否则为1.如1100|1010=1110 ~:0变1,1变0 ^:两边的位不同时，结果为1,否则为0.如1100^1010=0110 逻辑运算符 与（&&）、非（！）、或（||）
    
**四、赋值运算符**
= += -= *= /= %= &= ^= |= 《= 》=
    
**五、instanceof 运算符**
该运算符是双目运算符，左面的操作元是一个对象，右面是一个类。当左面的对象是右面的类创建的对象时，该运算符运算结果是 true,否则是 false.
    
**六、 运算符综述**
Java 的表达式就是用运算符连接起来的符合 Java 规则的式子。运算符的优先级决定了表达式中运算执行的先后顺序。例如，x<y&&!z 相当于（x<y）&&（！z），没有必要去记忆运算符号的优先级别，在编写程序时可尽量的使用括号来实现你想要的运算次序，以免产生难以阅读或含糊不清的计算顺序。

运算符的结合性决定了并列相同级别的运算符的先后顺序，例如，加减的结合性是从左到右，8-5+3 相当于（8-5）+3.逻辑否运算符 的结合性是右到左， x 相当于！（！x）。表3.4是Java 所有运算符的优先级和结合性。
    
**七 位移运算符**
《 带符号左移 》带符号右移 >>> 无号右移
例子：int a1 = 8; // 0000 0000 0000 1000   System.out.println（a1>>>2）； //// 0000 0000 0000 0010
输出为 2
运算符优先级
按优先级从高到低排列如下：[ ]、 （ ）、 ++、--、 !、 ~、 instanceof、 *、 /、 %、 +、 -、《、 》、 >>>、 <>、 < 、=、 >、 \、 ==、 !=、 &、^、& &、 ||、 ? :、= .

**Java 强制类型转换**
强制和转换
Java 语言和解释器限制使用强制和转换，以防止出错导致系统崩溃。整数和浮点数运算符间可以来回强制转换，但整数不能强制转换成数组或对象。对象不能被强制为基本类型。 Java 中整数运算符在整数运算时，如果操作数是 long 类型，则运算结果是 long 类型，否则为 int 类型，绝不会是 byte,short 或 char 型。这样，如果变量i被声明为 short 或 byte,i+1 的结果会是 int.如果结果超过该类型的取值范围，则按该类型的最大值取模。
    
**运算符操作**
一、运算符"+",如果必要则自动把操作数转换为 String 型。如果操作数是一个对象，它可定义一个方法 toString（）返回该对象的 String 方式，例如 floata=1.0print（"Thevalueofais"+a+"\n"）；+运算符用到的例子 Strings="a="+a;+= 运算符也可以用于 String.注意，左边（下例中的s1）仅求值一次。s1+=a;//s1=s1+a//若 a 非 String型，自动转换为 String 型。
二、整数算术运算的异常是由于除零或按零取模造成的。它将引发一个算术异常。下溢产生零，上溢导致越界。例如：加1超过整数最大值，取模后，变成最小值。一个 op= 赋值运算符，和上表中的各双目整数运算符联用，构成一个表达式。整数关系运算符<,>,<=,>=,==和！=产生 boolean 类型的数据。
三、数组运算符数组运算符形式如下：<expression>[<expression>]可给出数组中某个元素的值。合法的取值范围是从0到数组的长度减1.
四、对象运算符双目运算符 instanceof 测试某个对象是否是指定类或其子类的实例。
例如：if（myObjectinstanceofMyClass）  {  MyClassanothermyObject=（MyClass）myObject;  …  }
是判定 myObject 是否是 MyClass 的实例或是其子类的实例。
五、浮点运算符浮点运算符可以使用常规运算符的组合：如单目运算符++、--,双目运算符+、-、```*```和/,以及赋值运算符+=,-=,*=,和/=.此外，还有取模运算：%和%=也可以作用于浮点数，例如：a%b 和 a-（（int）（a/b）*b）的语义相同。这表示 a%b 的结果是除完后剩下的浮点数部分。只有单精度操作数的浮点表达式按照单精度运算求值，产生单精度结果。如果浮点表达式中含有一个或一个以上的双精度操作数，则按双精度运算，结果是双精度浮点数。
六、布尔运算符布尔（boolean）变量或表达式的组合运算可以产生新的 boolean 值，fales 和 true（记得是小写）。单目运算符！是布尔非。双目运算符&,|和^是逻辑 AND,OR 和 XOR 运算符，它们强制两个操作数求布尔值。为避免右侧操作数冗余求值，用户可以使用短路求值运算符&&和||.
七、用户可以使用==和！=,赋值运算符也可以用&=、|=、^=.三元条件操作符和 C 语言中的一样。
八、++运算符用于表示直接加1操作。增量操作也可以用加运算符和赋值操作间接完成。++lvalue（左值表示 lvalue+=1,++lvalue 也表示 lvalue=lvalue+1.
九、--运算符用于表示减1操作。++和--运算符既可以作为前缀运算符，也可以做为后缀运算符。双目整数运算符是：运算符操作**+加-减*乘/除%取模&位与|位或^位异或《左移 》右移（带符号） >>>添零右移整数除法按零舍入。除法和取模遵守以下等式： （a/b）*b+（a%b）==a
    
**java 运算符问题：**
&是位
&&是逻辑
当&两边是整数时执行的是位运算，而两边是 boolean 值时执行的是逻辑运算， 如： 3&6 就是执行的位运算，结果是一个整数：
2 true&false 执行的就是逻辑运算，结果是一个 boolean 值：false &的逻辑运算和&&逻辑运算是存在一定不同的
&逻辑运算时两边都会计算的，而&&则在左边为假时则直接返的是 false 不再计算右边
举个例子：
1:int[] a={1,2,3};   if（a[0]==2&a[3]==4）{System.out.println（"true"）}
2:int[] a={1,2,3};   if（a[0]==2&&a[3]==4）{System.out.println（"true"）}
这两个例子中，第一个会抛出异常，而第二个则什么不会输出也不会抛异常 这是因为第一个例子中 if 语句中用的是&,所以两边的都会计算，当计算a[3]==4时抛出数组下标越界异常。第二个例子则在计算第一个式子a[0]==2发现结果为假则不再计算右边，直接返回 false,所以该例子不会输出任何东西。