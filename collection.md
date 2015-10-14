# 集合类

# Java 集合类详解

# 集合类说明及区别

Collection
├List
│├LinkedList
│├ArrayList
│└Vector
│　└Stack
└Set
Map
├Hashtable
├HashMap
└WeakHashMap

## Collection 接口

Collection 是最基本的集合接口，一个 Collection 代表一组 Object，即 Collection 的元素（Elements）。一些 Collection 允许相同的元素而另一些不行。一些能排序而另一些不行。Java SDK 不提供直接继承自 Collection 的类，Java SDK 提供的类都是继承自 Collection的“子接口”如 List 和 Set。
　　
所有实现 Collection 接口的类都必须提供两个标准的构造函数：无参数的构造函数用于创建一个空的 Collection，有一个 Collection 参数的构造函数用于创建一个新的 Collection，这个新的 Collection 与传入的 Collection 有相同的元素。后 一个构造函数允许用户复制一个Collection。
　　
如何遍历 Collection 中的每一个元素？不论 Collection 的实际类型如何，它都支持一个iterator()的方法，该方法返回一个迭代子，使用该迭代子即可逐一访问 Collection 中每一个元素。典型的用法如下：

```
　　　　Iterator it = collection.iterator(); // 获得一个迭代子
　　　　while(it.hasNext()) {
　　　　　　Object obj = it.next(); // 得到下一个元素
　　　　}
```

由 Collection 接口派生的两个接口是 List 和 Set。

### List 接口
　　
List 是有序的 Collection，使用此接口能够精确的控制每个元素插入的位置。用户能够使用索引（元素在 List 中的位置，类似于数组下标）来访问 List 中的元素，这类似于 Java 的数组。

和下面要提到的 Set 不同，List 允许有相同的元素。
　　
除了具有 Collection 接口必备的 iterator()方法外，List 还提供一个 listIterator()方法，返回一个 ListIterator 接口，和标准的 Iterator 接口相比，ListIterator 多了一些 add()之类的方法，允许添加，删除，设定元素， 还能向前或向后遍历。
　　
实现 List 接口的常用类有 LinkedList，ArrayList，Vector 和 Stack。

### LinkedList 类
　　
LinkedList 实现了 List 接口，允许 null 元素。此外 LinkedList 提供额外的 get，remove，insert 方法在 LinkedList 的首部或尾部。这些操作使 LinkedList 可被用作堆栈（stack），队列（queue）或双向队列（deque）。
　　
注意 LinkedList 没有同步方法。如果多个线程同时访问一个 List，则必须自己实现访问同步。一种解决方法是在创建 List 时构造一个同步的 List：
　　　　
```
List list = Collections.synchronizedList(new LinkedList(...));
```

### ArrayList 类
　　
ArrayList 实现了可变大小的数组。它允许所有元素，包括 null。ArrayList 没有同步。
size，isEmpty，get，set 方法运行时间为常数。但是 add 方法开销为分摊的常数，添加 n 个元素需要 O(n)的时间。其他的方法运行时间为线性。
　　
每个 ArrayList 实例都有一个容量（Capacity），即用于存储元素的数组的大小。这个容量可随着不断添加新元素而自动增加，但是增长算法 并没有定义。当需要插入大量元素时，在插入前可以调用 ensureCapacity 方法来增加 ArrayList 的容量以提高插入效率。
　　
和 LinkedList 一样，ArrayList 也是非同步的（unsynchronized）。

### Vector 类
　　
Vector 非常类似 ArrayList，但是 Vector 是同步的。由 Vector 创建的 Iterator，虽然和  ArrayList 创建的 Iterator 是同一接口，但是，因为 Vector 是同步的，当一个 Iterator 被创建而且正在被使用，另一个线程改变了 Vector 的状态（例如，添加或删除了一些元素），这时调用 Iterator 的方法时将抛出 ConcurrentModificationException，因此必须捕获该异常。

### Stack 类
　　
Stack 继承自 Vector，实现一个后进先出的堆栈。Stack 提供5个额外的方法使得 Vector 得以被当作堆栈使用。基本的 push 和 pop 方法，还有 peek 方法得到栈顶的元素，empty 方法测试堆栈是否为空，search 方法检测一个元素在堆栈中的位置。Stack 刚创建后是空栈。

### Set 接口
　　
Set 是一种不包含重复的元素的 Collection，即任意的两个元素 e1 和 e2 都有 e1.equals(e2)=false，Set 最多有一个 null 元素。
　　
很明显，Set 的构造函数有一个约束条件，传入的 Collection 参数不能包含重复的元素。
　　
请注意：必须小心操作可变对象（Mutable Object）。如果一个 Set 中的可变元素改变了自身状态导致 Object.equals(Object)=true 将导致一些问题。

### Map 接口
　　
请注意，Map 没有继承 Collection 接口，Map 提供 key 到 value 的映射。一个 Map 中不能包含相同的 key，每个 key 只能映射一个 value。Map 接口提供3种集合的视图，Map 的内容可以被当作一组 key 集合，一组 value 集合，或者一组 key-value 映射。

### Hashtable 类
　　
Hashtable 继承 Map 接口，实现一个 key-value 映射的哈希表。任何非空（non-null）的对象都可作为 key 或者 value。
　　
添加数据使用 put(key, value)，取出数据使用 get(key)，这两个基本操作的时间开销为常数。

Hashtable 通过 initial capacity 和 load factor 两个参数调整性能。通常缺省的 load factor 0.75较好地实现了时间和空间的均衡。增大 load factor 可以节省空间但相应的查找时间将增大，这会影响像 get 和 put 这样的操作。

使用 Hashtable 的简单示例如下，将1，2，3放到 Hashtable 中，他们的 key 分别是”one”，”two”，”three”：

```
　　　　Hashtable numbers = new Hashtable();
　　　　numbers.put(“one”, new Integer(1));
　　　　numbers.put(“two”, new Integer(2));
　　　　numbers.put(“three”, new Integer(3));
```

要取出一个数，比如2，用相应的 key：

```
　　　　Integer n = (Integer)numbers.get(“two”);
　　　　System.out.println(“two = ” + n);
```

由于作为 key 的对象将通过计算其散列函数来确定与之对应的 value 的位置，因此任何作为 key的对象都必须实现 hashCode 和 equals 方法。hashCode 和 equals 方法继承自根类 Object，如果你用自定义的类当作 key 的话，要相当小心，按照散列函数的定义，如果两个对象相同，即 obj1.equals(obj2)=true，则它们的 hashCode 必须相同，但如果两个对象不同，则它们的 hashCode 不一定不同，如果两个不同对象的 hashCode 相同，这种现象称为冲突，冲突会导致操作哈希表的时间开销增大，所以尽量定义好的 hashCode()方法，能加快哈希表的操作。
　　
如果相同的对象有不同的 hashCode，对哈希表的操作会出现意想不到的结果（期待的 get 方法返回 null），要避免这种问题，只需要牢记一条：要同时复写 equals 方法和 hashCode 方法，而不要只写其中一个。

Hashtable 是同步的。

### HashMap 类
　　
HashMap 和 Hashtable 类似，不同之处在于 HashMap 是非同步的，并且允许 null，即 null value 和 null key。，但是将 HashMap 视为 Collection 时（values()方法可返回Collection），其迭代子操作时间开销和 HashMap 的容量成比例。因此，如果迭代操作的性能相当重要的话，不要将 HashMap 的初始化容量设得过高，或者 load factor 过低。

### WeakHashMap 类
　　
WeakHashMap 是一种改进的 HashMap，它对 key 实行“弱引用”，如果一个 key 不再被外部所引用，那么该 key 可以被 GC 回收。

# 总结
　　
如果涉及到堆栈，队列等操作，应该考虑用 List，对于需要快速插入，删除元素，应该使用LinkedList，如果需要快速随机访问元素，应该使用 ArrayList。
　　
如果程序在单线程环境中，或者访问仅仅在一个线程中进行，考虑非同步的类，其效率较高，如果多个线程可能同时操作一个类，应该使用同步的类。
　　
要特别注意对哈希表的操作，作为 key 的对象要正确复写 equals 和 hashCode 方法。
　　
尽量返回接口而非实际的类型，如返回 List 而非 ArrayList，这样如果以后需要将 ArrayList换成 LinkedList 时，客户端代码不用改变。这就是针对抽象编程。

# 同步性

Vector 是同步的。这个类中的一些方法保证了 Vector 中的对象是线程安全的。而 ArrayList 则是异步的，因此 ArrayList 中的对象并不是线程安全的。因为同步的要求会影响执行的效率，所以如果你不需要线程安全的集合那么使用 ArrayList 是一个很好的选择，这样可以避免由于同步带来的不必要的性能开销。

数据增长

从内部实现机制来讲 ArrayList 和 Vector 都是使用数组(Array)来控制集合中的对象。当你向这两种类型中增加元素的时候，如果元素的数目 超出了内部数组目前的长度它们都需要扩展内部数组的长度，Vector 缺省情况下自动增长原来一倍的数组长度，ArrayList 是原来的50%,所以最 后你获得的这个集合所占的空间总是比你实际需要的要大。所以如果你要在集合中保存大量的数据那么使用 Vector 有一些优势，因为你可以通过设置集合的初 始化大小来避免不必要的资源开销。

使用模式

在 ArrayList 和 Vector 中，从一个指定的位置（通过索引）查找数据或是在集合的末尾增加、移除一个元素所花费的时间是一样的，这个时间我们用 O(1)表示。但是，如果在集合的其他位置增加或移除元素那么花费的时间会呈线形增长：O(n-i)，其中 n 代表集合中元素的个数，i 代表元素增加或移除元素的索引位置。为什么会这样呢？以为在进行上述操作的时候集合中第 i 和第 i 个元素之后的所有元素都要执行位移的操作。这一切意味着什么呢？

这意味着，你只是查找特定位置的元素或只在集合的末端增加、移除元素，那么使用 Vector 或ArrayList 都可以。如果是其他操作，你最好选择其他的集合操作类。比如，LinkList 集合类在增加或移除集合中任何位置的元素所花费的时间都是一样的?O(1)，但它在索引一个元素的使用缺比较慢 －O(i),其中 i 是索引的位置.使用 ArrayList 也很容易，因为你可以简单的使用索引来代替创建 iterator 对象的操作。LinkList 也会为每个插入的元素创建对象，所有你要明白它也会带来额外的开销。

最后，在《Practical Java》一书中 Peter Haggar 建议使用一个简单的数组（Array）来代替 Vector 或 ArrayList。尤其是对于执行效率要求高的程序更应如此。因为使用数组 (Array)避免了同步、额外的方法调用和不必要的重新分配空间的操作。

# 相互区别

## Vector 和 ArrayList

1，vector 是线程同步的，所以它也是线程安全的，而 arraylist 是线程异步的，是不安全的。如果不考虑到线程的安全因素，一般用 arraylist 效率比较高。

2，如果集合中的元素的数目大于目前集合数组的长度时，vector 增长率为目前数组长度的100%,而 arraylist 增长率为目前数组长度的50%.如过在集合中使用数据量比较大的数据，用 vector 有一定的优势。

3，如果查找一个指定位置的数据，vector 和 arraylist 使用的时间是相同的，都是0(1),这个时候使用 vector 和 arraylist 都可以。而如果移动一个指定位置的数据花费的时间为 0(n-i)n 为总长度，这个时候就应该考虑到使用 linklist,因为它移动一个指定位置的数据所花费的时间为 0(1),而查询一个指定位置的数据时花费的时间为 0(i)。

ArrayList 和 Vector 是采用数组方式存储数据，此数组元素数大于实际存储的数据以便增加和插入元素，都允许直接序号索引元素，但是插入数据要设计到数组元素移动 等内存操作，所以索引数据快插入数据慢，Vector 由于使用了 synchronized 方法（线程安全）所以性能上比ArrayList 要差，LinkedList 使用双向链表实现存储，按序号索引数据需要进行向前或向后遍历，但是插入数据时只需要记录本项的前后项即可，所以插入数度较快！

## arraylist 和 linkedlist

1.ArrayList 是实现了基于动态数组的数据结构，LinkedList 基于链表的数据结构。
2.对于随机访问 get 和 set，ArrayList 觉得优于 LinkedList，因为 LinkedList 要移动指针。
3.对于新增和删除操作 add 和 remove，LinedList 比较占优势，因为 ArrayList 要移动数据。
这一点要看实际情况的。若只对单条数据插入或删除，ArrayList 的速度反而优于 LinkedList。但若是批量随机的插入删除数据，LinkedList 的速度大大优于 ArrayList. 因为 ArrayList 每插入一条数据，要移动插入点及之后的所有数据。

## HashMap 与 TreeMap
(注)
文章出处：http://www.diybl.com/course/3_program/java/javaxl/200875/130233.html

1、HashMap 通过 hashcode 对其内容进行快速查找，而 TreeMap 中所有的元素都保持着某种固定的顺序，如果你需要得到一个有序的结果你就应该使用 TreeMap（HashMap 中元素的排列顺序是不固定的）。

HashMap 中元素的排列顺序是不固定的）。

2、HashMap 通过 hashcode 对其内容进行快速查找，而 TreeMap 中所有的元素都保持着某种固定的顺序，如果你需要得到一个有序的结果你就应该使用 TreeMap（HashMap 中元素的排列顺序是不固定的）。集合框架”提供两种常规的 Map 实现：HashMap 和 TreeMap (TreeMap 实现SortedMap 接口)。

3、在 Map 中插入、删除和定位元素，HashMap 是最好的选择。但如果您要按自然顺序或自定义顺序遍历键，那么 TreeMap 会更好。使用 HashMap 要求添加的键类明确定义了 hashCode()和  equals()的实现。　　这个 TreeMap 没有调优选项，因为该树总处于平衡状态。

结过研究，在原作者的基础上我还发现了一点，二树 map 一样，但顺序不一样，导致 hashCode()不一样。
同样做测试：
在 hashMap 中，同样的值的 map,顺序不同，equals 时，false;
而在 treeMap 中，同样的值的 map,顺序不同,equals 时，true，说明，treeMap 在 equals()时是整理了顺序了的。

## hashtable 与 hashmap

一.历史原因:Hashtable 是基于陈旧的 Dictionary 类的，HashMap 是 Java 1.2 引进的 Map 接口的一个实现

二.同步性:Hashtable 是线程安全的，也就是说是同步的，而 HashMap 是线程序不安全的，不是同步的

三.值：只有 HashMap 可以让你将空值作为一个表的条目的 key 或 value