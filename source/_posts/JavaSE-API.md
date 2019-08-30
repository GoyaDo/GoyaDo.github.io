---
title: JavaSE-API
date: 2017-08-25 16:15:23
update: 2017-12-16
tags: [Java基础入门]
categories:
 - JavaSE常用API
keywords: java入门,JavaSE基础语法,常用API,String,StringBuffer
description: JavaSE常用API
comments:
password:
copyright: true
---
# JavaSE-常用API

## GregorianCalendar类

Date类用来表示时间点，并且官方目前推荐用GregorianCalendar类

GregorianCalendar类用来表示更为通用的日历表示法

GregorianCalendar类扩展一个更通用的Calendar类，这个类描述了日历的一般属性

### 构造器

new GregorianCalendar():构造一个新对象，用于表示对象构造时的日期和时间。

new GregorianCalendar(1999，11，31):用给定日期和时间构造一个Gregorian日历对象

要想查询某个时间点的年月日等信息，应该使用GregorianCalendar类的get方法，为了表达希望得到的项，需要借助于Calendar类中定义的一些常量，比如Calendar.Month或Calendar.DAY_OF_WEEK;

还有设置年月日的set方法。

get方法和set、add方法在概念上有区别，get方法仅仅查看并返回对象的状态，而set和add方法却对对象的状态进行修改。对实例域做出修改的方法称为更改器方法，仅访问实例域而不进行修改的方法称为访问其方法。

### 常用方法

void add(int field, int amount):对给定的时间域增加指定数量的时间

int getFirstDayOfWeek():获得当前用户所在地区，一个星期中的第一天。

void setTime(Date time):将日历设置为指定的时间点.

Date getTime():获得这个日历对象当前值所表达的时间点

String[]getShortWeekdays()

String[]getShortMonths ()

String[]getWeekdays()

String[]getMonths ()

获得当前地区的星期几或几月份的名称，利用Calendar的星期和月份常量作为数组索引值.

### Calendar类

它为特定瞬间与一组诸如YEAR、MONTH、DAY_OF_MONTH、HOUR等日历字段之间的转换提供了一些方法，并为操作日历字段

```java
public int get (int field)://返回给定日历字段的值，日历类中的每个日历字段都是静态的成员变量，并且时int类型
public void add(int field,int amount)://根据给定的日历字段和对应的时间，来对当前的日历进行操作
public final void set(int year,int month,int date)://设置当前日历的年月日
```



## Object类

可以使用Object类型的变量引用任何类型的对象，Object类型的变量只能用于作为各种值得通用持有者。要想对其中的内容进行具体的操作，还需要清楚对象的原始类型，并进行相应的类型转换。

在Java中，只有基本类型不是对象。所有的数组类型都属于Object类。

构造方法：public Object()

### hashCode()方法

散列码(hash code)是由对象导出的一个整数值,散列码是没有规律的。hashCode方法定义在Object类中，每个对象都有一个默认的散列码,其值为对象的存储地址.

int hash(Object…objects):返回一个散列码，由提供的所有对象的散列码组合而得到。

``` java
public class ObjectDemo{
  public void main(String[] args){
    Phone p = new Phone();
    System.out.println(p.hashCode());//11299397
    Phone p2 = new Phone();
    System.out.println(p2.hashCode());//24446859
    Phone p3 = p1;
    System.out.println(p3.hashCode());//11299397
  }
}
```

### getClass()方法

```
public final  Class <？> getClass（）
```

返回此运行时类Object返回的 Class对象是由static synchronized所表示的类的方法锁定的对象。

**实际结果的类型是Class<? extends |X|> 其中|X|是静态类型上其表达的擦除getClass被调用。**例如，此代码片段中不需要强制转换：

`Number n = 0; `
`Class<? extends Number> c = n.getClass();`

返回：

在`Class`表示运行时类此对象的对象。在`Class`表示运行时类此对象的对象。

###  toString()方法

返回对象的字符串表示，默认是由类的全路径+'@'+哈希值的十六进制表示

```
public  String  toString()
```

返回对象的字符串表示形式。通常，该 toString方法返回一个“文本表示”此对象的字符串。结果应该是一个简洁但信息丰富的表示，便于人们阅读。建议所有子类都重写此方法。

toString类 的方法Object返回一个字符串，该字符串由对象为实例的类的名称，符号字符“ @`”和对象的哈希码的无符号十六进制表示组成。换句话说，此方法返回一个等于值的字符串：

```java
getClass().getName()+'@'+ Integer.toHexString(hashCode())
```

- 返回：

  对象的字符串表示形式。

```java
//Integer类下的一个静态方法
public static String toHexString(int i);//把一个整数转成一个十六进制表示的字符串
```

一般toString()方法返回的值是没有意义的，所以我们需要对其重写，一般在子类重写该方法

建议把该类的所有成员变量值组成返回即可，也可以根据自己需求

### equals()方法

```
public boolean equals（Object  obj）
```

指示某个其他对象是否“等于”此对象。

该equals方法在非null对象引用上实现等价关系：

- 它是*自反的*：对于任何非空引用值 x，x.equals(x)应该返回 true。
- 它是*对称的*：对于任何非空引用值 x和y，x.equals(y)应该返回true当且仅当 y.equals(x)回报true。
- 它是*传递*性：对于任何非空的参考值 x，y以及z，如果 x.equals(y)回报率true和 y.equals(z)回报率true，那么 x.equals(z)应该返回true。
- 它是*一致的*：对于任何非空引用值 x以及一致返回 或一致返回的y多次调用 ，前提是不修改在对象比较中使用的信息。 x.equals(y) true false equals
- 对于任何非空引用值x， x.equals(null)应返回false。

equals类 的方法Object实现了对象上最具辨别力的等价关系; 即，对于任何非空的参考值x和 y，该方法返回true当且仅当x和y指代相同的对象（x == y具有值true）。

请注意，通常需要在重写此hashCode方法时覆盖该方法，以便维护该hashCode方法的常规协定，该协定声明相等的对象必须具有相等的哈希代码。

#### equals方法的常用格式：

1. 显示参数命名为otherObject，稍后需要将他转换成另一个叫做other的变量。

2. 检测this与otherObject是否引用同一个对象:

   `if(otherObject== null) return false;`

3. 比较this与otherObject是否属于同一个类，如果equals的语义在每个子类中有所改变，就是用getClass检测:

   `if(getClass()!=otherObject.getClass())return false;`

   如果所有子类都拥有统一的语义，就使用instanceof检测:

   `if(!otherObjectinstanceof ClassName)) return false;`

4. 将otherObject转换为相应的类型变量:

   `ClassNameother = (ClassName)otherObject`

5. 使用==比较基本类型域，使用equals比较对象域，如果都匹配，返回true，否则返回false

   `returnfield1 == other.field1&&Object.equals(field2,other.field2)&&.. .;`

6. 如果在子类中重新定义equals，就要在其中包含调用super.equals(other)

**equals方法指示其他某个对象是否与此对象"相等".这个方法默认情况下比较的是地址值，比较地址值一般来说意义不大，所以需要重写该方法，一般用来比较对象的成员变量值是否相同**

> ==：
>
> 基本类型：比较的就是值是否相同
>
> 引用类型：比较的就是地址值是否相同

demo:

``` java
public boolean equals(Object obj){
  //return true
  //这里改进phone的equals方法，根据这里比较的成员变量决定返回true或false
  //因为name是String类型，所以不能用==比较，应该用equals
  //String类的equals方法是重写Object类的，比较的是字符串内容是否相同
  //我们比较的是手机类的成员变量，所以要向下转型
  Phone p = (Phone)obj;
  if(this.name.equals(p.name) && this.size == p.size){
    return true;
  }else{
    return false;
  }
}
```

### finalize()方法

确定不存在对该对象的更多引用时，由于对象的垃圾回收器调用此方法。用于垃圾回收，但是什么时候回收不知道

当垃圾回收器

protected void finalize（）throw Throwable

> 当垃圾收集确定没有对该对象的更多引用时，由对象上的垃圾收集器调用。子类重写finalize处置系统资源或执行其他清理的方法。

> 一般合同finalize是，如果Java TM虚拟机确定不再有任何方法可以通过任何尚未死亡的线程访问此对象，则会调用它，除非采取了一些操作通过最终确定一些其他准备完成的对象或类。该finalize方法可以采取任何动作，包括使该对象再次可用于其他线程; finalize然而，通常的目的是在对象被不可撤销地丢弃之前执行清理操作。例如，表示输入/输出连接的对象的finalize方法可能会执行显式I / O事务，以在永久丢弃对象之前断开连接。

> finalize类 的方法不Object执行特殊操作; 它只是正常返回。子类 Object可以覆盖此定义。

> Java编程语言不保证哪个线程将为finalize任何给定对象调用该方法。但是，可以保证，调用finalize时，调用finalize的线程不会持有任何用户可见的同步锁。如果finalize方法抛出未捕获的异常，则忽略该异常并终止该对象的终止。

> 在finalize为一个对象调用该方法之后，在Java虚拟机再次确定不再有任何方法可以通过任何尚未死亡的线程访问该对象之前不再采取任何操作，包括可能的操作准备好最终确定的其他对象或类，此时可以丢弃该对象。

> finalize对于任何给定对象，Java虚拟机永远不会多次调用该方法。

> 该finalize方法抛出的任何异常都会导致暂停此对象的终结，但会被忽略。

> 抛出：
>
> Throwable- Exception通过这种方法提出的

### clone()方法

protected  Object  clone（）throw CloneNotSupportedException

Cloneable:此类实现了Cloneable接口，以指示Object.clone()方法可以合法的对该类实例进行按字段赋值，这个接口是个标记接口，告诉我们实现该接口就可以实现对象的复制了

创建并返回此对象的副本。“复制”的确切含义可能取决于对象的类别。一般意图是，对于任何对象x，表达式：
 x.clone（）！= x
将是真的，那表达式：
 x.clone（）。getClass（）== x.getClass（）
会true，但这些不是绝对的要求。通常情况是：
 x.clone（）。等于（x）的
将是true，这不是一个绝对的要求。
按照惯例，返回的对象应该通过调用获得 super.clone。如果一个类及其所有超类（除了 Object）遵守这个约定，那将是这种情况 x.clone().getClass() == x.getClass()。

按照惯例，此方法返回的对象应独立于此对象（正在克隆）。要实现此独立性，可能需要在返回super.clone之前修改返回的对象的一个​​或多个字段。通常，这意味着复制包含被克隆对象的内部“深层结构”的任何可变对象，并使用对副本的引用替换对这些对象的引用。如果一个类只包含原始字段或对不可变对象的引用，那么通常情况下super.clone 不需要修改返回的对象中的任何字段。

clone类 的方法Object执行特定的克隆操作。首先，如果此对象的类未实现接口Cloneable，则 CloneNotSupportedException抛出a。请注意，所有数组都被认为是实现接口，Cloneable并且clone数组类型方法的返回类型T[] 是T[]T是任何引用或基本类型。否则，此方法创建此对象的类的新实例，并使用该对象的相应字段的内容初始化其所有字段，就像通过赋值一样; 这些字段的内容本身不会被克隆。因此，该方法执行该对象的“浅拷贝”，而不是“深拷贝”操作。

该类Object本身并不实现接口 Cloneable，因此clone在类的对象上调用该方法Object将导致在运行时抛出异常。

返回：
这个实例的克隆。
抛出：
CloneNotSupportedException- 如果对象的类不支持该Cloneable接口。覆盖该clone方法的子类也可以抛出此异常以指示无法克隆实例。

要想实现对象克隆，那么对象所在的类需要实现一个Cloneable接口

## Scanner类

System类下有一个静态的字段

`public static final InputStream in;`标准的输入流，对应着键盘输入

`InputStream is = System.in`

``` java
Class Demo{
  public static final int x = 10;
  public static final Phone p = new Phone();
}
int y = Demo.x;
Phone p = Demo.p;
//构造方法
Scanner(InputStream source);
//基本用法
Scanner sc = new Scanner(System.in);
int x = sc.nexInt();
```

#### Scanner类的成员方法

基本格式:

hasNextXxx()：判断是否还有下一个输入项，其中Xxx可以是Int，Double等，如果需要判断是否包含下一个字符串则可以省略Xxx

nextXxx()：获取下一个输入想，Xxx和上面的方法中Xxx相同

默认情况下，Scanner使用空格，回车等作为分隔符

常用方法

public int nextInt()

public String nextLine()

## String 类

字符串是由多个字符组成的一串数据，也可以看成是一个字符数组。

- 字符串字面值“abc“也可以看成是一个字符串对象
- 字符串是常量，一旦被赋值，就不能被改变
  - 字符串的内容不能改变，而不是引用不能改变

``` java
String  a = "123";

String b = "123";

a  == b ;true

//因为引用的是同一个123

```

#### 堆内存里有个字符串常量池->本质是一个数组

`String s = "123";`
池中没有新的数据则添加数据，如果有，则指向
在采用直接赋值过程中，对于字符串而言可以实现池数据的自动保存，这样如果再有相同数据定义时，减少想通过对象产生，提升操作性能

`String s = new String("123");`
开辟两块堆内存空间，而只会使用一块，而另外一个由于字符串常量所定义的匿名对象会成为垃圾空间
实际上是属于一种自己专用的内存空间，但是在String类里面也提供有帮助开发者实现手工入池

#### 两种方法的区别:

1->只会产生一个实例化对象，并且可以自动保存到对象池中，以实现该字符串实例的重用

2->会产生两个实例化对象，并且不会自动入池，无法对对象重用，但是可以利用intern()方法手工入池

#### String对象(常量)池

对象池的主要目的是实现数据的共享处理，以Spring对象池为例，里面的内容主要就是为了重用，重用就是为了共享设计，但是在在Java之中对象（常量）池实际上可分为两种

**静态常量池：**

指的是程序(.*class)在加载时候会自动将此程序之中保存的字符串、普通的常量、类和方法的信息等等，全部进行分配;

**运行时常量池：**

指的是程序(.*class)加载之后，里面可能有一些变量，这个时候提供的常量池。

#### 空串和Null串:

空串有自己的串长度和内容，String变量可以存放一个特殊的值，名为null，有时候要检查一个字符串既不是null也不为空串，需要使用

if(str !=null &&str.length()!= 0)    

#### 构造方法

``` java
public String()://空构造
public String(byte[] bytes)://把字节数组转成在字符串
public String(byte[] bytes,int index,int length)://把字节数组的一部分转成字符串
public String(char[] value)://把字符数组转成字符串
public String(char[] value,int index,int count)://把字符数组的一部分转成字符串
public String(String original)://把字符串常量值转成字符串
```

#### 面试题

```java
//看程序写结果
//字符串如果是变量相加，先开空间，再拼接
//字符串如果是常量相加，是先加，然后在常量池找，如果有就直接返回，否则就创建
String s1 = "hello";
String s2 = "world";
String s3 = "helloworld";
System.out.println(s3 == s1+s2);//false
System.out.println(s3.equals(s1+s2));//true
//通过反编译可知，这里已经做了处理
System.out.println(s3 =="hello"+"world");//true-->s3=="helloworld"
System.out.println(s3.equals("hello"+"world"));//true-->s3.equals("helloworld")
```

#### String类的判断功能

```java
boolean equals(Object obj)://比较字符串的内容是否相同，区分大小写
boolean equalsIgnoreCase(String str)://比较字符串的内容是否相同，忽略大小写
boolean contains(String str)://判断大字符串中是否包含小字符串
boolean startWith(String str)://判断字符串是否以某个指定的字符串开头
boolean endsWith(String str)://判断字符串是否以某个指定的字符串结尾
boolean isEmpty()://判断字符串是否为空
//注意：字符串内容为空和字符串对象为空
String s = "";
String s = null;
```

#### String类的获取功能

``` java
int length()://获取字符串的长度
char charAt(int index)://获取指定索引位置的字符
int indexOf(int ch)://返回指定字符在此字符串中第一次出现处的索引
//在这里是int类型而不是char类型，是因为'a'和97都可以代表'a'
int indexOf(Stirng str)://返回指定字符出中第一次出现处的索引
int indexOf(int ch,int fromIndex)://返回指定字符串在此字符串中从指定位置后第一次出现处的索引
int indexOf(String str,int fromIndex)://返回指定字符串在此字符串中从中指定位置后第一次出现处的索引
String substring(int start)://从指定位置开始截取字符串，默认到末尾
String substring(int start,int end)://从指定位置开始到指定位置结束截取字符串
```

#### 字符串的遍历

``` java
for(int x = 0;x<s.length();x++){
  System.out.println(s.charAt(x));
}
```

#### 统计大小写个数案例

``` java
//定义一个字符串
String s = "Hello123World";
//定义三个统计变量
int bigCount = 0;
int smallCount = 0;
int numberCount = 0;
//遍历字符串，得到每一个字符
for(int x = 0;x<s.length();x++){
  char ch = s.charAt(x);
  //判断该字符到底属于那种类型
  if(ch>='a' && ch<='z'){
    smallCount++;
  }else if(ch>='A' && ch<='Z'){
    bigCount++;
  }else if(ch>='0' && ch<='9'){
    numberCount++;
  }
}
//输出结果
System.out.println("大写字母"+bigCount+"个");
System.out.println("小写字母"+smallCount+"个");
System.out.println("数字"+numberCount+"个");
```

#### String类的转换功能

``` java
byte[] getBytes()://把字符串转换为字节数组
char[] toCharArray()://把字符串转换为字符数组
static String valueOf(char[] chs)://把字符数组转成字符串
static String valueOf(int i)://把int类型的数组转成字符串,注意：String类的valueOf()方法可以把任意类型的数据转成字符串
String toLowerCase()://把字符串转成小写
String toUpperCase()://把字符串转成大写
String concat(String str)://把字符串拼接
```

##### 字符串首字母大写，其他转小写

```java
String result = s.substring(0,1).toUpperCase().concat(s.substring(1).toLowerCase());
```

#### String类的其他功能

##### String类的替换功能

``` java
String replace(char old,char new);
String replace(String old,String new);
```

##### 去除字符串两空格

``` java
String trim();
```

##### 按字典顺序比较两个字符串

``` java
int compareTo(String str);
int compareToIgnoreCase(String str);
String s1 = "hello";
String s2 = "hello";
String s3 = "abc";
String s4 = "xyz";
System.out.println(s1.compareTo(s2));//0
System.out.println(s1.compareTo(s3));//7
System.out.println(s1.compareTo(s4));//-16至于这里为什么是-16，可以想想
```

##### int数组拼接成字符串案例

``` java
//两个明确：返回值类型：String 参数列表：int[] arr
public static String arrayToString(int[] arr){
  //定义一个字符串
  String s = "";
  //先把字符串拼接一个"["
  s += "[";
  //遍历int数组，得到每一个元素
  for(int x = 0; x < arr.length;x++){
    //先判断该元素是否是最后一个
    if(x==arr.length-1){
      //是就直接拼接元素和"]"
      s +=arr[x];
      s += "]";
    }else{
      //拼接元素和逗号以及空格
      s += arr[x];
      s += ", ";
    }
  }
  return s;
}
```

##### 字符反转

```java
//两个明确，返回值类型：String 参数列表：String
public static String myReverse(String s){
  //定义一个新字符串
  String result = "";
  //把字符串转成字符数组
  char[] chs = line.toCharArray();
  //倒着遍历字符串，得到每一个字符
  for(int x = chs.length-1;x>=0;x--){
    //用新字符串把每一个字符拼接起来
    result += chs[x];
  }
  return result;
}
```

##### 在大串中查找小串出现的次数案例

```java
public static void main(String[] args){
  //定义大串
  String maxString="woaijavazhenaijavawoaizhavazhenaijava";
  //定义小串
  String minString="java";
  //功能实现
  int count = getCount(maxString,minString);
  System.out.println("java在大串中出现了"+count+"次");
}
private static int getCount(String maxString,String minString){
  //定义一个统计变量，初始值是0
  int count = 0;
  int index;
  //先查，赋值，判断
  while((index = maxString.indexOf(minStirng))!=-1){
    count++;
    maxString = maxString.subString(index+minString.length());
  }
  return count;
}
```

##### 格式化字符串

字符串  ->  %s
字   符  ->  %c
整   数  ->  %d
小   数  ->  %f

## StringBuffer类

线程安全的可变字符串

StringBuffer和String的区别

StringBuffer长度和内容可变，String不可变

如果使用StringBuffer做字符串的拼接，不会浪费太多的资源

### StringBuffer类的构造方法

```java
public StringBuffer()://无参构造方法
public StringBuffer(int capacity)://指定容量的字符串缓冲区对象
public StringBuffer(String str)://指定字符串内容的字符串缓冲区对象

//StringBuffer的方法
public int capacity()://返回当前容量，理论值
public int length()://返回长度(字符数)，实际值
```

### StringBuffer的添加功能

```java
public StringBuffer append(String str)://可以把任意类型数据添加到字符串缓冲区里面，并返回字符串缓冲区本身
public StringBuffer insert(int offset,String str)://在指定位置把任意类型的数据插入到字符串缓冲区里面，并返回字符串缓冲区本身
```

### StringBuffer的删除功能

```java
public StringBuffer deleteCharAt(int index)://删除指定位置的字符，并返回本身
public StringBuffer delete(int start,int end)://删除从指定位置开始指定位置结束的内容，并返回本身
```

### StringBuffer的替换功能

```java
public StringBuffer replace(int start,int end,String str)://从start开始到end用str替换
```

### StringBuffer的反转功能

```java
public StringBuffer reverse()
```

### StringBuffer的截取功能

```java
//在这里返回值类型是String
public String substring(int start);
public String substring(int start,int end);
```

### String和StringBuffer的相互转换

```java
//String --> StringBuffer
String s = "hello";
//方法1，通过构造方法
StringBuffer sb = new StringBuffer(s);
//方法2，通过append方法
String Buffer sb2 = new StringBuffer();
sb2.append(s);

//StringBuffer --> String
StringBuffer buffer = new StringBuffer("java");
//方法1，通过构造方法
String str = new String(buffer);
//方法2，通过toString()方法
String str2 = buffer.toString();
```

### 用StringBuffer做数组拼接指定格式字符串

```java
public static String arrToString2(int[] arr){
  StringBuffer sb = new StringBuffer();
  sb.append("[")；
    for(int x = 0;x<arr.length;x++){
      if(x == arr.length-1){
        sb.apend(arr[x]);
      }else{
        sb.append(arr[x]).append(", ");
      }
    }
  sb.append("]");
  return sb.toString();
}
```

### 字符串反转功能

```java
public static String myReverse2(String s){
  return new StringBuffer(s).reverse().toString();
}
```

### 判断一个字符串是否对称

```java
public static boolean isSame(String s){
  boolean flag = true;
  //把字符串转成字符数组
  char[] chs = s.toCharArray();
  for(int start = 0,end = chs.length-1;start<=end;start++,end--){
    if(chas[start]!=chs[end]){
      return false;
    }
  }
  return true;
}
```

### String,StringBuffer,StringBuilder的区别

String是内容不可变的，StringBuffer，StringBuilder是内容可变的

StringBuffer是同步的，数据安全，效率低，StringBuilder是不同步的，数据不安全，效率高

String作为参数传递，效果和基本类型作为参数传递是一样的，形式参数的改变不影响实际参数

**StringBuffer和数组的区别？**

二者都可以看出是一个容器，装其他的数据

但是，StringBuffer的数据最终是一个字符串数据

而数组可以放置多种数据，但必须是同一种数据类型

## Arrays类

Arrays：针对数组进行操作的工具类，比如说排序和查找

```java
public static String toString(int[] a)://把数组转成字符串
public static void sort(int[] a)://对数组进行排序
public static int binarySearch(int[] a,int key)://二分查找

```

## 基本包装类

所有的基本类型都有一个与之对应的类，这些类称为包装器:Integer、Long、Double、Short、Byte、Character、Void、Boolean。前六个类派生于公共的超类Number。对象包装器类是不可变的，一旦构造了包装器，就不允许更改包装在其中的值，同时，包装器类还是final，因此不能定义它们的子类。

自动装箱:    list.add(3);

list.add(Integer.valueOf(3));

自动拆箱:    int n = list.gei(i);

Int n = list.gei(i).intValue(); 

参数数量可变的方法:

```java
public static void double max(double… values){
…
}
```

为了对基本数据类型进行更多的操作，更方便的操作，Java就针对每一种基本数据类型提供了对应的类类型，包装类类型

byte -->Byte

short --> Short

int --> Integer

long --> Long

float --> Float

double --> Double

char --> Character

boolean --> Boolean

### Integer的构造方法

```java
public Integer (int value)
public Integer(String s)
//这里这个字符出啊必须是由数字字符组成
```

### String和int类型的相互转换

```java
int --> String
String.valueOf(number)
String --> int
Integer.parseInt(s)
```

### Integer中进制转换的操作

```java
//常用的基本进制转换
public static String toBinaryString(int i);
public static String toOctalString(int i);
public static String toHexString(int i);

//十进制到其他进制
public static String toString(int i,int radix);
//其他进制到十进制
public static int parseInt(String s,int radix);
```

### JDK5自动装箱和拆箱

自动装箱：把基本类型转换为包装类类型

自动拆箱：把包装类类型转换为基本类型

**注意：**

在使用Integer x = null;代码机会出现NullPointerException，建议先判断是否为null，然后再使用

Integer的数据直接赋值，如果在-128到127之间，会直接从缓冲池里获取数据

### Character

Character类在对象中包装一个基本类型char的值

该类提供了几种方法，以确定字符的类型（小写字母，数字，等等），并将字符从大写转换成小写，反之亦然

构造方法：`Character(char value)`

```java
public static boolean isUpperCase(char ch)://判断给定的字符是否是大写字符
public static boolean isLowerCase(char ch)://判断给定的字符是否是小写字符
public static boolean isDigit(char ch)://判断给定的字符是否是数字字符
public static char toUpperCase(char ch)://把给定的字符转换为大写字符
public static char toLowerCase(char ch)://把给定的字符转换为小写字符
```

## Math类

用于数学运算的类

```java
//成员变量
public static final double PI
public static final double E
//成员方法
public static int abs(int a)://绝对值
public static double ceil(double a)://向上取整
public static double floor(double a)://向下取整
public static int max(int a,int b)://最大值
public static double pow(double a,double b)://a的b次幂
public static double random()://随机数[0.0,1.0)
public static int round(float a)://四舍五入
public static double sqrt(double a)://正平方根
```

### 获取任意范围内的随机数

```java
public class MathDemo{
  public static void main(String[] args){
    Scanner sc = new Scanner(System.in);
    System.out.println("请输入开始数:");
    int start = sc.nextInt();
    System.out.println("请输入结束数:");
    int end = sc.nextInt();
    
    for(int x = 0;x<100;x++){
      //调用功能
      int num = getRandom(start,end);
      //输出结果
      System.out.println(num);
    }
  }
  //返回值类型：int 参数列表int start，int end
  public static int getRandom(int start,int end){
    int number = (int)(Math.random()*end)+start;
    return number;
  }
}
```

## Random类

产生随机数的类

``` java
//构造方法
public Random()://没有给种子，用的是默认种子，是当前时间的毫秒值
public Random(long seed)://给出指定的种子
//给定种子后，每次得到的随机数是相同的
//成员方法
public int nextInt()://返回的是int范围内的随机数
public int nextInt(int n)://返回的是[0,n)范围内的随机数
```

## System类

System类包含一些有用的类字段和方法，它不能被实例化

```java
//方法
public static void gc()://运行垃圾回收器，等同于调用了Runtime里的gc()
public static void exit(int status)://终止当前正在运行的Java虚拟机，参数用作状态码；根据惯例，非0的状态码表示异常终止
public static long currentTimeMillis()://返回以毫秒为单位的当前时间
public static arraycopy(Object src,int srcPos,Object dest,int destPos,int length)://从指定源数组中复制一个数组，复制从指定的位置开始，到目标数组的指定位置结束
```

## BigInteger类

可以让超过Integer范围内的数据进行运算

```java
//构造方法
BigInteger(String val);
//方法
public BigInteger add(BigInteger val)://加
public BigInteger subtract(BigInteger val)://减
public BigInteger multiply(BigInteger val)://乘
public BigInteger divide(BigInteger val)://除
public BigInteger[] divideAndRemainder(BigInteger val)://返回商和余数的数组
```

## BigDecimal类

不可变的、任意精度的有符号十进制数，可以解决数据丢失问题

```java
//构造方法
public BigDecimal(String val);
//方法
public BigDecimal add(BigDecimal val)://加
public BigDecimal subtract(BigDecimal augend)://减
public BigDecimal multiply(BigDecimal subtrahend)://乘
public BigDecimal divide(BigDecimal multipicand)://除
public BigDecimal[] divide(BigDecimal divisor,int scale,int roundingMode)://返回商和余数的数组
```

## Date类

表示特定的瞬间，精确到毫秒

```java
//构造方法
Date()://根据当前的默认毫秒值创建日期对象
Date(long date)://根据给定的毫秒值创建日期对象
//方法
public long getTime()://获取时间，以毫秒为单位
public void setTime(long time)://设置时间

//从Date得到一个毫秒值
  //getTime()
//把一个毫秒值转换为Date
  //构造方法
  //setTime(long time)
```

### DateFormat类实现日期和字符串的相互转换

``` java
//Date --> String(格式化)
public final String format(Date date);
//String -->Date(解析)
public Date parse(String source);

//DateFormat:可以进行日期和字符串的格式化和解析，但是由于是抽象类，所以使用具体子类SimpleDateFormat
//SimpleDateFormat的构造方法
SimpleDateFormat()://默认模式
SimpleDateFormat(String pattern)://给定的模式
//这个模式的字符串(年-y，月-M，日-d，时-H，分-m，秒-s)
```

```
Date date = new Date();
SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss.SSS");
String str = sdf.format(date);
System.out.println(str);
```
`parse()`:解析字符串

## UUID类

是一种生成无重复字符串的一种程序类，这种程序类的主要功能是根据时间戳实现一个自动的无重复的字符串定义

`UUID.randomUUID();`

## Optional类

进行null的相关处理，在以前进行程序开发的时候，如果为了防止程序中出现空指向的异常，可以以追加有null的验证。

在引用接受的一方往往都是被动的进行判断，在Java中提供Optional这个类，可以实现null的处理操作

``` java
public static <T> Optional<T>empty(); //返回空数据
public T get();//获取数据
public static <T> Optional<T> of(T value); //保存数据，但是不允许出现null.如果在保存数据时候存在null，则会抛出NullPointerException异常
public static <T> Optional<T> ofNullable(T value); //保存数据，允许为空
public T orElse(T other); //空的时候返回其它数据
```

## ThreadLocal类

解决线程同步问题
在ThreadLocal类里面存放两个对象，一个线程对象，一个数据对象

```java
//操作数据对象：
public ThreadLocal();//构造方法
public void set(T value);//设置数据
public T get();//取出数据
public void remove();//删除数据
```

 每一个线程通过ThreadLocal只允许保存一个数据

## Base64加密与解密

 Base64类里面有两个内部类:

```java
//Base64.Encoder:进行加密处理
public byte[] encode(byte[] src);
//Base64.Decoder:进行解密处理
public byte[] decode(String src);
```
## 比较器

### Comparable

 比较器

`public int ComparTo();`

### Comparator

挽救型比较器

## CharSequence接口

三个常用子类
String  StringBuffer StringBuilder

描述的是一个字符串

## AutoCloseable接口

日资源开发的处理，以实现资源的自动关闭（释放资源)
jdk1.7后，该接口只有一个方法:

`public void close() throws Exception`

除了实现这个接口，还得实现异常处理，要跟异常捆绑在一起

## Runtime类

描述运行时状态，是唯一一个与JVM运行状态有关的类，并且都会默认提供有一个该类的实例化对象
构造方法私有，单类设计模式，
`getRuntime()`  获取实例化对象
`availableProcessors()` 方法可以获取本机的CPU内核数
`maxMermory()` 获取最大内存空间，默认配置本机系统内存的四分之一
`totalMemory()` 获取可用内存空间，默认配置本机系统内存六十四分之一
`freeMemory()` 获取空闲内存空间
`gc()` 手工进行GC处理

垃圾收集器，是可以由系统自动调用垃圾释放功能，也可以自己手工调用

## Cleanner类

进行finialize()方法替代
在新一代的清除回收处理的过程之中，更多情况下考虑的是多线程的使用，即，为了防止有可能造成的延迟处理，许多对象回收前的处理都是单独通过一个线程完成的





































