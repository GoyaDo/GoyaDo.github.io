---
title: JavaWeb-JSP
date: 2018-03-15
tags: [JavaWeb]
categories:
- JavaWeb
- JSP
keywords: javaweb入门,JSP
description: JSP
comments:
password:
copyright: true
---

# JSP

JSP就是一种包装的Servlet

## **JSP和Servlet的分工**

**JSP:**

* 作为请求发起页面，例如显示表单、超链接
* 作为请求结束页面，例如显示数据

**Servlet:**

* 作为请求中处理数据的环节
* 获取JSP发送过来的请求参数
* 处理请求，得到处理后的数据
* 把结果保存到request域中
* 转发到显示结果的JSP

## **JSP的组成**

JSP=html+java脚本+jsp标签(指令)

## **JSP九大内置对象**

request-->HttpServletRequest
response-->HttpServletResponse
sessio-->HttpSession
applicatio-->servletContext类的对象
pageContext-->页面上下文对象
config-->ServletConfig
out-->输出流，用来向客户端响应
page-->当前jsp的"this"，真身Object
exception-->Throwable

**pageContext**

Servlet中有三大域：request、response、application
Jsp中有四大域:request、response、application、pageContext
servletCotext:整个应用程序
session:整个会话（一个会话中只有一个用户）
request：一个请求链
pageContext：一个jsp页面！这个域是在当前jsp页面和当前jsp页面中使用的标签之间共享数据
域对象
代理其他域：pageContext.setAttribute("xxx","xxx",PageContext.SESSION.SCOPE);
全域查找：pageContext.findAttribute("xxx");从小到大，依赖查找
获取其他8个内置对象
## **3种Java脚本**

<%...%>java代码片段，用于定义0~N条Java语句。方法内写什么，它写什么
<%= ...%>java表达式，用于输出，输出一条表达式的结果。response.getWrite().print(...)这里能放什么，它就能放什么
<%!...%>声明，用来创建类的成员和变量方法，class MyClass{}（类体）这里能放什么它放什么
JSP输出
<%-- ... --%>当服务器把JSP编译成java文件时已经忽略了注释部分

<%@ ...%> jsp指令，也是一种特殊的标签

## **JSP原理**

JSP其实就是一种特殊的Servlet
当jsp页面第一次被访问时，服务器会把jsp编译成java文件（这个java其实是一个servlet)类
然后再把java编译成.class
然后创建该类对象
最后调用它的service()方法
第二次请求同一jsp时，直接调用service()方法

tomcat的work目录下可以找到jsp对应的.java源代码

## JSP标签

**JSP三大指令：**
指令格式:<%@ ... %>

**page:最复杂**

* pageEncoding和ContentType：
  * pageEncoding:指定当前jsp页面的编码，只要不说谎就不会乱码,在服务器要把jsp编译成.java需要使用pageEncoding
  * ContentType：添加一个响应头，等同于response.setContentType("text/html;charset=utf-8"):

如果两个属性只提供一个，那么另一个的默认值为设置那一个。
如果两个都没设置，默认时iso

* import:导包
* errorPage和isErrorPage：
  * errorPage：当前页面抛出异常，那么要转发到哪一个页面，由errorPage来指定（请求转发）
  * isErrorPage：当前页面是否为处理错误的页面，当该属性为true时，这个页面会设置状态码为500，而且这个页面可以使用9大内置对象中的exception。

 **web.xml中配置错误页面**

```xml
<error-page>
	<error-code>404</error-code>
	<location>/error404.jsp</location>
</error-page>
<error-page>
	<error-code>500</error-code>
	<location>/error500.jsp</location>
</error-page>
<error-page>
	<exception-type>java.lang.RuntimeException</exception-type>
	<location>/error.jsp</location>
</error-page>
```

 **autoFlush和buffer**

* autoFlush:指定jsp输出缓冲区满时，是否自动刷新，默认时true，如果为false，那么在缓冲区满时抛出异常
* buffer:指定缓冲区大小，默认为8kb，通常不需要修改
* isELIgnored:是否忽略el表达式，默认值为false，不忽略，支持
* language:指定当前jsp编译后的语言类型，默认值为java
* info：信息
* isThreadSafe：默认为false，是否支持并发访问
* session:当前页面是否支持session，如果false，则当前页面没有session内置对象
* extends:让jsp生成的servlet去继承该属性指定的类

**include:静态包含**   
与RequestDispatcher的include()方法的功能相似
<%@include%>：它是在jsp编译成java文件时完成的，共同生成一个java文件（一个Servlet），再生成一个class
RequestDispatcher的include()方法：包含和被包含的是两个servlet，即两个.class它们只是把响应的内容在运行时合并了
作用：把不变的和变得分开

**taglib:导入标签库**
prefix:指定标签库在本页中的前缀，由我们自己来起名字
uri：指定标签库的位置

**JSP动作标签**
是由服务器来解释执行
html提供的标签由浏览器来执行

```java
<jsp:forward>:与RequestDispatcher的forward方法是一样的，一个在Servlet中使用，一个在JSP中使用
<jsp:include>:与RequestDispatcher的include方法是一样的，一个在Servlet中使用，一个在JSP中使用
<%@include%>和<jsp:include>的不同，前者是两者包含在一起，后者是仅仅把输出结果合并
<jsp:param>:作为forward和include的子标签，用来给转发或包含的页面传递参数
```


tomcat cof目录下 context.xml
`<Context reloadable="true">`:不用重启tomcat

JSP其实是一个servlet，在conf下的web.xml里看到有个JspServlet，调用jsp页面则是调用这个JspServlet，把jsp文件读取变成.java,然后编译成.class，然后创建其对象，调用其service方法

## EL表达式

EL是JSP内置的表达式语言，可以全域查找${xxx}
如果查找不到，输出空字符串，不是null
（pageContext-->request-->session-->application）

```java
${pageContextScope.xxx}

${requestScope.xxx}

${session.xxx}

${application.xxx}
```

jsp2.0开始不让使用java脚本，而是使用el表达式和动态标签来替代java脚本
EL替代的是<%=...%>,也就是说EL只能做输出

**JavaBean导航：**

```javascript
${requestScope.emp.address.street}得到这个bean里的街道

<!--request.getAttribute("emp").getAddress().getStreet() -->

```

EL可以输出的东西都在11个内置对象中！11个内置对象，其中10个是Map，pageContext不是map，它就是PageContext类型

EL可以输出的东西都在11个内置对象中！11个内置对象，其中10个是Map，pageContext不是map，它就是PageContext类型

param和paramValues这两个内置对象是用来获取请求参数的
**param：** `Map<String,String>`类型，param对象可以用来获取参数，与request.getParameter()方法相同 ，key时参数名，value是参数值，适用于单值的参数 
map.key是el的语法
map['key']也可以操作map 
**paramValues：** paramValues是`Map<String,String[]>`类型，当一个参数名，对应多个参数值时可以使用它

**header：** 对应请求头，是一个Map，其中key表示头名称，value是个单个头值，适用于单值请求头
 ${header['User-Agent']}
**headerValues：** 对应请求头，是一个Map，其中key表示头名称，value是多个头值，适用于多值请求头

**initParam：** 获取`<context-param>`内的参数

**Cookie：** `Map<String,Cookie>`类型，key是Cooke的name，value是cookie对象
${cookie.username.value}获取值

**pageContext：** 它是pageContext类型${pageContext.request.contextPath}

***EL函数库***
EL函数库是由第三方对EL的扩展，由JSTL提供
EL函数库就是定义一些有返回值的静态方法
因为是第三方，所以需要导入，导入需要talib指令
导入标签库`<%@ taglib prefix="fu" uri="http://java.sun.com/jsp/jstl/functions"%>`

```java
String toUpperCase(String input);//参数转大写

String toLowerCase(Stirng input);//参数转小写

int indexOf(String input,String substring);//大串输出小串位置

boolean contains(String input,String substring);//大串是否包含小串

boolean containsIgnoreCase(String input,String substring);//忽略大小写，是否包含

boolean startsWith(String input,String substring);//是否以小串为前缀

boolean endsWIth(String input,String subString);//是否以小串为后缀

String subString(String input,int beginIndex,int endIndex);//截取字串

String subStringAfter(String input,String substring);//获取大串中，小串在位置后面的字符串

String subStringBefore(String input,String substring);//获取大串中，小串所在位置前面的字符串

String escapeXml(String input):把input中字符串的">""<"//转义

String trim(String input);//去除前后空格

String replace(String input,String substringBefore,String substringAfter);//替换

String[] split(String input,String delimiters);

int length(Object obj);//可以获取字符串、数组、各种集合的长度

String join(String array[],String separator);//联合字符串数组

```

**自定义EL函数库**
写一个类，写一个有返回值的静态方法
编写***.tld文件，可以参数fn.tld文件来写，把xxx.tld文件放到/WEB-INF目录下

```xml
<function>
    <name>fun</name>
    <function-class>cn.cj.fn.MyFunction</function-class>
    <function-signature>java.lang.String fun()</function-signature>
</function>
```

在页面中添加taglib指令，导入自定义标签库
${cj: fun()};

## JSTL标签

1. jstl的概述
  * apache的东西，依赖EL
  * 使用jstl需要导入jstl1.2.jar
  * 四大库：
    > core：核心库，重点
    > fmt：格式化：日期、数字
    > sql：过时
    > xml：过时

2. 导入标签库
  * jar包
  * 在jsp页面中：<%@taglib prefix="前缀" uri="路径"%>

core --> c标签！

1. out和set
  * <c:out>：输出
    > value：可以是字符串常量，也可以是EL表达式
    > default：当要输出的内容为null时，会输出default指定的值
    > escapeXml：默认值为true，表示转义！
  * <c:set>：设置(创建域的属性)
    > var：变量名
    > value：变量值，可以是EL表达式
    > scope：域，默认为page，可选值：page、request、session、application

2. remove
  * <remove>：删除域变量
    > var：变量名
    > scope：如果不给出scope，表示删除所有域中的该名称的变量；如果指定了域，那么只删除该域的变量。

3. url
  * value：指定一个路径！它会在路径前面自动添加项目名。
    <> `<c:url value="/index.jsp"/>`，它会输出/day13_1/index.jsp

  * 子标签：`<c:param>`，用来给url后面添加参数，例如：

    ```javascript
    <c:url value="/index.jsp">
      <c:param name="username" value="张三"/>  <!--可以对参数进行url编码！！-->
    </c:url>
    ```

    结果为：/day13_1/index.jsp?username=%ED%2C%3F%ED%2C%3F
  * var：指定变量名，一旦添加了这个属性，那么url标签就不会再输出到页面，而是把生成url保存到域中。

  * scope：它与var一起使用，用来保存url。

4. if：对应java中的if语句
  * `<c:if test="布尔类型">...</c:if>`，当test为值时，执行标签体内容！

5. choose：它对应java中的if/else if/ ... /else
  * 例如：

    ```javascript
    c:choose
      <c:when test="">.../c:when
      <c:when test="">.../c:when
      <c:when test="">.../c:when
       ... 
      c:otherwise .../c:otherwise
    /c:choose
    ```

    等同与
    if(...) {
    } else if( ....) {
    } else if( ....) {
    } else if( ....) {
    } ...
    else { ...}

6. forEach
  它用来循环遍历数组、集合！
  它还可以用来计数方式来循环！

  计数方式：

  for(int i = 1; i <= 10; i++) {
    ...
  }

  ```javascript
  <c:forEach var="i" begin="1" end="10">
    ${i}
  </c:forEach>
  ```

  属性：
    * var：循环变量
    * begin：设置循环变量从几开始。
    * end：设置循环变量到几结束。
    * step：设置步长！等同与java中的i++，或i+=2。step默认为1

用来输出数组、集合！

```javascript
<c:forEach items="${strs }" var="str">
 ${str }<br/>
</c:forEach>
```

等同于

for(String str : strs) {
  ...
}

属性：
* items：指定要循环谁，它可以是一个数组或一个集合
* var：把数组或集合中的每个元素赋值给var指定的变量。

循环状态

可以使用varStatus来创建循环状态变量！

循环状态变量有如下属性：
  * count：循环元素的个数
  * index：循环元素的下标
  * first：是否为第一个元素
  * last：是否为最后一个元素
  * current：当前元素

```javascript
<c:forEach items="${list }" var="ele" varStatus="vs">
    ${vs.index} ${vs.count } ${vs.first } ${vs.last } ${vs.current }<br/>
</c:forEach>
```

fmt库
  它是格式化库

`<fmt:formatDate value="" pattern="">`

value：指定一个Date类型的变量
pattern：用来指定输出的模板！例如：yyyy-MM-dd HH:mm:ss

`<fmt:formatNumber value="${num1}" pattern="0.00">`
  保留小数点后2位，它会四舍五入！如果不足2位，以0补位！

`<fmt:formatNumber value="${num1}" pattern="#.##">`
  保留小数点后2位，它会四舍五入！如果不足2位，不补位！

**自定义标签**

1. 步骤
  * 标签处理类（标签也是一个对象，那么就需要先有类！）
  * tld文件，它是一个xml
  * 页面中使用`<%@taglib%>`来指定tld文件的位置

2. 标签处理类
  SimpleTag接口：
  * void doTag()：每次执行标签时都会调用这个方法；
  * JspTag getParent()：返回父标签（非生命周期方法）
  * void setParent(JspTag)：设置父标签
  * void setJspBody(JspFragment)：设置标签体
  * void seetJspContext(JspContext)：设置jsp上下文对象，它儿子是PageContext

　　其中doTag()会在其他三个方法之后被tomcat调用。

3. 配置tld文件

tld文件一般都放到WEB-INF之下，这样保证客户端访问不到！

```xml
  <tag>
  	<name>myTag1</name> 指定当前标签的名称
  	<tag-class>cn.itcast.tag.MyTag1</tag-class> 指定当前标签的标签处理类！
  	<body-content>empty</body-content> 指定标签体的类型，我们这里使用的是空标签！
  </tag>
```

4. 页面中指定tld文件位置

<%@ taglib prefix="it" uri="/WEB-INF/tlds/itcast-tag.tld" %>
导标签库，就是为页面指定tld文件的位置！

进阶

标签体内容
  * empty：无标签体！
  * JSP：jsp2.0已经不在支持这个类型了！表示标签体内容可以是：java脚本，可以是标签，可以是el表达式
  * scriptless：只能是EL表达式，也可以是其他的标签！
  * tagdependent：标签体内容不会被执行，而是直接赋值标签处理类！

不在执行标签下面内容的标签！

在标签处理类中的doTag()中使用SkipPageException来结束！
　　Tomcat会调用标签处理类的doTag()方法，然后Tomcat会得到SkipPageException，它会跳过本页面其他内容！

标签属性

步骤：
1. 给你的标签处理类添加属性！
    为标签处理类添加属性，属性至少要且一个set方法！这个set方法会在doTag()方法之前被tomcat执行！所在doTag()中就可以使用属性了。

2. 在tld文件中对属性进行配置

   ```xml
   <attribute>
          	<name>test</name> <!--指定属性名-->
          	<required>true</required> <!--指定属性是否为必需的-->
          	<rtexprvalue>true</rtexprvalue> <!--指定属性是否可以使用EL-->
   </attribute>

   ```

推荐博文：

[JavaWeb](https://www.cnblogs.com/xdp-gacl/tag/JavaWeb%E5%AD%A6%E4%B9%A0%E6%80%BB%E7%BB%93/)

