# 字符串与数组

# Java 语言基础知识之字符串数组

java 语言中，数组是一种最简单的复合数据类型。数组是有序数据的集合，数组中的每个元素具有相同的数据类型，可以用一个统一的数组名和下标来唯一地确定数组中的元素。数组有一维数组和多维数组。

### 2.4.1 一维数组

1． 一维数组的定义

```
　　type arrayName[ ]；
　　类型(type)可以为Java中任意的数据类型，包括简单类型和复合类型。
　　例如：
　　　int intArray[ ]；
　　　Date dateArray[];
```

2．一维数组的初始化

```
　　◇ 静态初始化
　　　　int intArray[]={1,2,3,4};
　　　　String stringArray[]={"abc", "How", "you"};

　　◇ 动态初始化 
　　　 1）简单类型的数组
　　　　int intArray[]; 
　　　　intArray = new int[5];

　　　2）复合类型的数组
　　　　String stringArray[ ];
　　　　String stringArray = new String[3];/*为数组中每个元素开辟引用
　　　　　　　　　　　　　　　　　　　　　 空间(32位) */
　　　　stringArray[0]= new String("How");//为第一个数组元素开辟空间 
　　　　stringArray[1]= new String("are");//为第二个数组元素开辟空间
　　　　stringArray[2]= new String("you");// 为第三个数组元素开辟空间
```

3．一维数组元素的引用

数组元素的引用方式为：

```
　　　　　arrayName[index]
```

index 为数组下标，它可以为整型常数或表达式，下标从0开始。每个数组都有一个属性 length 指明它的长度，例如：intArray.length 指明数组 intArray 的长度。

### 2.4.2 多维数组

Java 语言中，多维数组被看作数组的数组。

1．二维数组的定义

```
　　type arrayName[ ][ ]；
　　type [ ][ ]arrayName;
```

2．二维数组的初始化

```
　　◇ 静态初始化
　　int intArray[ ][ ]={{1,2},{2,3},{3,4,5}};

　　Java语言中，由于把二维数组看作是数组的数组，数组空间不是连续分配的，所以不要求二维数组每一维的大小相同。

　　◇ 动态初始化
　　1) 直接为每一维分配空间，格式如下：
　　arrayName = new type[arrayLength1][arrayLength2];
　　int a[ ][ ] = new int[2][3]；

　　2) 从最高维开始，分别为每一维分配空间：
　　arrayName = new type[arrayLength1][ ];
　　arrayName[0] = new type[arrayLength20];
　　arrayName[1] = new type[arrayLength21];
　　…
　　arrayName[arrayLength1-1] = new type[arrayLength2n];

　　3) 例：
　　二维简单数据类型数组的动态初始化如下,
　　int a[ ][ ] = new int[2][ ]；
　　a[0] = new int[3];
　　a[1] = new int[5];
```

对二维复合数据类型的数组，必须首先为最高维分配引用空间，然后再顺次为低维分配空间。
而且，必须为每个数组元素单独分配空间。

例如：

```
　　String s[ ][ ] = new String[2][ ];
　　s[0]= new String[2];//为最高维分配引用空间
　　s[1]= new String[2]; //为最高维分配引用空间
　　s[0][0]= new String("Good");// 为每个数组元素单独分配空间
　　s[0][1]= new String("Luck");// 为每个数组元素单独分配空间
　　s[1][0]= new String("to");// 为每个数组元素单独分配空间
　　s[1][1]= new String("You");// 为每个数组元素单独分配空间
```

3．二维数组元素的引用
　　
对二维数组中的每个元素，引用方式为：arrayName[index1][index2]
例如： num[1][0];

4．二维数组举例：

【例2．2】两个矩阵相乘

```
　　public class MatrixMultiply{
　　　public static void main(String args[]){
　　　int i,j,k;
　　　int a[][]=new int [2][3]; //动态初始化一个二维数组
　　　int b[][]={{1,5,2,8},{5,9,10,-3},{2,7,-5,-18}};//静态初始化
　　　　　　　　　　　　　　　　　　　　　　　　　　 一个二维数组
　　　int c[][]=new int[2][4]; //动态初始化一个二维数组
　　　for (i=0;i<2;i++)
　　　　　for (j=0; j<3 ;j++)
　　　　　　a[i][j]=(i+1)*(j+2);
　　　for (i=0;i<2;i++){
　　　　　for (j=0;j<4;j++){
　　　　　　c[i][j]=0;
　　　for(k=0;k<3;k++)
　　　　　c[i][j]+=a[i][k]*b[k][j];
　　　　　　}
　　　　　}
　　　System.out.println("*******Matrix C********");//打印Matrix C标记
　　　for(i=0;i<2;i++){
　　　　　for (j=0;j<4;j++)
　　　　　　System.out.println(c[i][j]+" ");
　　　　　System.out.println();
　　　　　　}
　　　　　}
　　　}
```

## 2.5 字符串的处理

### 2.5.1 字符串的表示

Java 语言中，把字符串作为对象来处理，类 String 和 StringBuffer 都可以用来表示一个字符串。(类名都是大写字母打头)

```
　1．字符串常量

　　字符串常量是用双引号括住的一串字符。
　　　　"Hello World!"

　2．String 表示字符串常量

　　用String表示字符串：
　　String( char chars[ ] );
　　String( char chars[ ], int startIndex, int numChars );
　　String( byte ascii[ ], int hiByte );
　　String( byte ascii[ ], int hiByte, int startIndex, int numChars );
　　String 使用示例：
　　String s=new String() ; 生成一个空串

　　下面用不同方法生成字符串"abc"：
　　char chars1[]={'a','b','c'};
　　char chars2[]={'a','b','c','d','e'};
　　String s1=new String(chars1);
　　String s2=new String(chars2,0,3);
　　byte ascii1[]={97,98,99};
　　byte ascii2[]={97,98,99,100,101};
　　String s3=new String(ascii1,0);
　　String s4=new String(ascii2,0,0,3);

　3．用 StringBuffer 表示字符串

　　StringBuffer( ); /*分配16个字符的缓冲区*/
　　StringBuffer( int len ); /*分配 len 个字符的缓冲区*/
　　StringBuffer( String s ); /*除了按照s的大小分配空间外,再分配16个
　　　　　　　　　　　　　　　字符的缓冲区*/
```

### 2.5.2 访问字符串

1．类 String 中提供了 length( )、charAt( )、indexOf( )、lastIndexOf( )、getChars( )、getBytes( )、toCharArray( )等方法。

```
　　◇ public int length() 此方法返回字符串的字符个数
　　◇ public char charAt(int index) 此方法返回字符串中 index 位置上的字符，其中index 值的 范围是 0~length-1
　　◇ public int indexOf(int ch)
　　 　public lastIndexOf(in ch)
　　
　　返回字符 ch 在字符串中出现的第一个和最后一个的位置
　　◇ public int indexOf(String str)
　　　 public int lastIndexOf(String str)
　　返回子串 str 中第一个字符在字符串中出现的第一个和最后一个的位置 
　　◇ public int indexOf(int ch,int fromIndex)
　　　 public lastIndexOf(in ch ,int fromIndex)
　　返回字符 ch 在字符串中位置 fromIndex 以后出现的第一个和最后一个的位置
　　◇ public int indexOf(String str,int fromIndex)
　　　 public int lastIndexOf(String str,int fromIndex)
　　返回子串 str 中的第一个字符在字符串中位置 fromIndex 后出现的第一个和最后一个的位置。
　　◇ public void getchars(int srcbegin,int end ,char buf[],int dstbegin)
　　 srcbegin 为要提取的第一个字符在源串中的位置， end 为要提取的最后一个字符在源串中的位置，字符数组 buf[]存放目的字符串，　　　 dstbegin 为提取的字符串在目的串中的起始位置。 
　　◇public void getBytes(int srcBegin, int srcEnd,byte[] dst, int dstBegin)
　　参数及用法同上，只是串中的字符均用8位表示。
```

2．类 StringBuffer 提供了 length( )、charAt( )、getChars( )、capacity()等方法。

方法 capacity()用来得到字符串缓冲区的容量，它与方法 length()所返回的值通常是不同的。

### 2.5.3 修改字符串

修改字符串的目的是为了得到新的字符串，类 String 和类 StringBuffer 都提供了相应的方法。有关各个方法的使用，参考 java 2 API。

```
　1．String 类提供的方法：

　　　concat( )
　　　replace( )
　　　substring( )
　　　toLowerCase( )
　　　toUpperCase( )

　　◇ public String contat(String str);
　　用来将当前字符串对象与给定字符串str连接起来。
　　◇ public String replace(char oldChar,char newChar);
　　用来把串中出现的所有特定字符替换成指定字符以生成新串。
　　◇ public String substring(int beginIndex)；
　　public String substring(int beginIndex,int endIndex);
　　用来得到字符串中指定范围内的子串。
　　◇ public String toLowerCase();
　　把串中所有的字符变成小写。
　　◇ public String toUpperCase();
　　把串中所有的字符变成大写。
```

```
　2．StringBuffer 类提供的方法：

　　append( )
　　insert( )
　　setCharAt( )

　　如果操作后的字符超出已分配的缓冲区,则系统会自动为它分配额外的空间。
　　◇ public synchronized StringBuffer append(String str);
　　用来在已有字符串末尾添加一个字符串 str。
　　◇ public synchronized StringBuffer insert(int offset, String str);
　　用来在字符串的索引offset位置处插入字符串 str。
　　◇ public synchronized void setCharAt(int index,char ch);
　　用来设置指定索引 index 位置的字符值。 

　　注意：String 中对字符串的操作不是对源操作串对象本身进行的，而是对新生成的一个源操作串对象的拷贝进行的，其操作的结果不影响源串。

　　相反，StringBuffer 中对字符串的连接操作是对源串本身进行的，操作之后源串的值发生了变化，变成连接后的串。
```

### 2.5.4 其它操作

1．字符串的比较

String 中提供的方法：
equals( )和 equalsIgnoreCase( )
它们与运算符'= ='实现的比较是不同的。运算符'= ='比较两个对象是否引用同一个实例，而equals( )和 equalsIgnoreCase( )则比较两个字符串中对应的每个字符值是否相同。

2．字符串的转化

java.lang.Object 中提供了方法 toString( )把对象转化为字符串。

3．字符串"+"操作

运算符'+'可用来实现字符串的连接：
String s = "He is "+age+" years old.";
其他类型的数据与字符串进行"+"运算时，将自动转换成字符串。具体过程如下：
String s=new StringBuffer("he is").append(age).append("years old").toString();

注意：除了对运算符"+"进行了重载外，java 不支持其它运算符的重载。

【本讲小结】

java 中的数据类型有简单数据类型和复合数据类型两种，其中简单数据类型包括整数类型、浮点类型、字符类型和布尔类型；复合数据类型包含类、接口和数组。表达式是由运算符和操作数组成的符号序列，对一个表达式进行运算时，要按运算符的优先顺序从高向低进行，同级的运算符则按从左到右的方向进行。条件语句、循环语句和跳转语句是 java 中常用的控制语句。

数组是最简单的复合数据类型，数组是有序数据的集合，数组中的每个元素具有相同的数据类型，可以用一个统一的数组名和下标来唯一地确定数组中的元素。Java 中，对数组定义时并不为数组元素分配内存，只有初始化后，才为数组中的每一个元素分配空间。已定义的数组必须经过初始化后，才可以引用。数组的初始化分为静态初始化和动态初始化两种，其中对复合数据类型数组动态初始化时，必须经过两步空间分配：首先，为数组开辟每个元素的引用空间；然后，再为每个数组元素开辟空间。Java 中把字符串当作对象来处理， java.lang.String 类提供了一系列操作字符串的方法，使得字符串的生成、访问和修改等操作容易和规范。