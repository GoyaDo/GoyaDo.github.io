---
title: JavaWeb-Servlet
date: 2018-03-12
tags: [JavaWeb]
categories:
- JavaWeb
- Servlet
keywords: Servlet
description: Servlet
comments:
password:
copyright: true
---

# Servlet

每个Servlet都是唯一的，它们处理的请求都是不同的
浏览器把请求发送给不同的Servlet。Servlet是异步的线程不安全的。
单例，一个类只有一个对象

## **Servlet调用过程？**

1.  在浏览器输入地址，浏览器先去查找hosts文件，将主机名翻译为ip地址，如果找不到就再去查询dns服务器将主机名翻译成ip地址。
2.  浏览器根据ip地址和端口号访问服务器，组织http请求信息发送给服务器。
3.  服务器收到请求后首先根据Host请求头判断当前访问的是哪台虚拟主机。
4.  服务器根据http请求头中的请求URI判断当前访问的是哪个web应用。
5.  服务器根据http请求头中的请求URI判断当前访问的是web应用中的哪个web资源。
6.  检查web应用的web.xml文件，如果根据路径找到具体的servlet处理类的全路径名交给该servlet处理,如果找不到就交给缺省servlet处理。
7.  这个过程中浏览器只知道自己发出来http请求，不久就收到了http响应，浏览器不知道也不关心服务器内部是如何处理的。浏览器和服务器之间的关系是非常单纯的，只有HTTP协议。
8.  解析请求、封装RequestResponse对象、创建Servlet、调用Service方法都是服务器自动进行的，开发人员只需要写好Servlet配置进容器中即可，无需操心具体的底层实现。

## **实现Servlet的方式：**

实现javax.servlet.Servlet接口

## **生命周期方法**
init(); 会在Servlet对象创建之后马上执行，并且执行一次
service()； 会被调用多次，每次处理请求都是在调用这个方法
destroy()；会在Servlet被销毁之前调用，并且只会被调用一次
ServletConfig()；获取Servlet配置信息
getServletInfo()；获取Servlet的信息
继承javax.servlet.GenericServlet类
继承javax.servlet.http.HttpServlet类
Servlet中的方法大多数不由我们来调用，而是由Tomcat来调用，并且Servlet的对象也由Tomcat来创建

## **如何让浏览器访问Servlet**

给Servlet指定一个Servlet路径（让Servlet与一个路径绑定在一起）
需要在web.xml中队Servlet进行配置

```xml
<servlet>
	<servlet-name>AServlet</servlet-name>
	<servlet-class>java.test.web.AServlet</servlet-class>
	<init-param>
		<param-name>p1</param-name>
		<param-value>v1</param-value>
	</init-param>
</servlet>
<servlet-mapping>
	<servlet-name>AServlet</servlet-name>
	<url-pattern>/AServlet</url-pattern>
</servlet-mapping>
```

 浏览器访问Servlet路径

## **ServletConfig**
1个ServletConfig对象，对应一段web.xml中Servlet的配置信息
String getServletName():获取  `<servlet-name></servlet-name>`
ServletContext getServletContext():获取Servlet上下文对象
String getInitParameter(String name):通过名称获取指定初始化参数的值
Enumeration getInitParameterNames()：获取所有初始化参数的名称

## **GenericServlet**

```java
public class BServlet extends GenericServlet {
    private ServletConfig config;
    @Override
    public void service(ServletRequest arg0, ServletResponse arg1) throwsServletException, IOException {
    }
    @Override
    public void destroy() {
         super.destroy();
    }
    @Override
    public String getInitParameter(String name) {
         return this.config.getInitParameter(name);
    }
    @Override
    public Enumeration<String> getInitParameterNames() {
         return super.getInitParameterNames();
    }
    @Override
    public ServletConfig getServletConfig() {
         return this.config;
    }
    @Override
    public ServletContext getServletContext() {
         return this.config.getServletContext();
    }
    @Override
    public String getServletInfo() {
         return super.getServletInfo();
    }
    @Override
    public String getServletName() {
         return this.config.getServletName();
    }
    @Override
    public void init() throws ServletException {
    }
    @Override
    public void init(ServletConfig config) throws ServletException {
         this.config=config;
         init();
    }
}
```

```java
public class CServlet extends BServlet {
    @Override
    public void init() throws ServletException {
    }
    @Override
    public void service(ServletRequest arg0, ServletResponse arg1) throwsServletException, IOException {
         String value = super.getInitParameter("p1");
    }
}

```

## **HttpServlet**

```java
HttpServlet extends GenderServlet{
    void service(ServletRequest,ServletResponse)-->生命周期方法
    //强转两个参数为http协议相关的类型
    //调用本类的
    void service(HttpServletRequest,HttpServletResponse)-->参数已经是Http协议相关的，使用起来更加方便
    //它会通过request得到当前请求方式，例如：GET或POST
    //根据请求方式再调用doGet()或doPost()方法
    void doGet(){...}重写
    void doPost(){...}重写
    //doGet和doPost由自己覆盖，如果没有覆盖，并且它们被调用了，那么会出现405
}
```

## **Servlet细节**
Servlet只有一个实例对象，那么就有可能出现一个Servlet同时处理多个请求，那么Servlet就不是线程安全的，这说明Servlet的工作效率很高，但也存在线程安全问题
所以我们不应该Servlet中创建成员变量，因为可能会存在一个线程对这个成员进行写操作，另外一个线程对这个成员进行读操作
可以创建局部变量
可以创建无状态成员
可以创建有状态成员，但成员是可读的（去掉set方法）

让服务器在启动时就创建Servlet
默认情况下，服务器会在某个Servlet第一次请求时创建它，也可以在web.xml中对Servlet进行配置，使服务器启动时就创建Servlet
在`<servlet>`中配置`<load-on-startup>`(一个非负整数)`</load-on-startup>`

`<url-pattern></url-pattern>`
早期达到过滤功能给出多个url-pattern
通配符：路径匹配 ：/serlvet/* ，可以匹配任何前缀后缀
扩展名匹配 * .do
/* ：都匹配
"* " 只能在两端不能在中间

## **conf下的web.xml**
default:优先级最低，如果一个请求没人处理，它处理-->404
jsp是jspServlet处理的
session的过期时间是30min
## **Servlet与反射**
访问Servlet，通过url-pattern找到，然后name匹配找到地址，反射拿到class

## **ServletContext**
一个项目只有一个ServletContext对象
我们可以在多个Servlet中来获取这个唯一的对象，使用它可以给多个Servlet传递数据
在tomcat启动时创建，在tomcat关闭死去
服务器为每个应用创建一个ServletContext对象：

ServletContext对象的创建是在服务器启动时完成的
ServletContext对象的销毁是在服务器关闭时完成的
在整个web应用的动态资源之间共享数据
获取ServletContext对象

```java
this.getServletConfig.getServletContext();
this.getServletContext();
       
ServletConfig#getServletContext();
GenericServletContext()#getServletContext();
HttpSession#getServletContext();
ServletContextEvent#getServletContext();
```

## **域对象的功能**
ServletContext是JavaWeb四大域对象之一，域对象就是用来在多个Servlet中传递数据，域对象必须有要存储数据的功能，有取数据的功能
四大域对象：PageContext,ServletRequest,HttpSession,ServletContext
域对象内部有一个Map，用来存储数据
ServletContext操作数据的方法：
void setAttribute(String name Object value):用来存储一个对象，也可以称之为存储一个域属性，如果多次调用该方法，并且使用相同的name，那么会覆盖上一次的值，这一特性与Map相同
Object getAttribute(String name):用来获取ServletContext中的数据
void removeAttribute(String name):用来移出ServletContext中的域属性，如果不存在，则什么都不做
Enumeration getAttributeNames():获取所有域属性的名称

## **获取应用初始化参数**
Servlet也可以获取初始化参数，但是它是局部参数，也就是说，一个Servlet只能获取自己的初始化参数，不能获取别人的，即初始化参数只为一个Servlet准备
可以配置公共的初始化参数，为所有的Servlet而用，使用ServletContext使用

```xml
<context-param>
    <parm-name></parm-name>
    <parm-value></parm-value>
</context-param>
```
得到ServletContext
调用getInitParameter(String)得到初始化参数

## **获取资源路径**

获取真实路径
String path = this.getServletContext().getRealPath("");
得到的是有盘符的路径F:/xxx/xxx/xx
获取资源的路径后，创建流对象
this.getServletContext().getResourceAsStream("/index.jsp");
获取当前路径下所有资源的路径
this.getServletContext().getResourcePaths("/WEB-INF")

## **获取类路径下的资源**
获取类路径资源，对javaweb项目而言，就是/WEB-INF/classes和/WEB-INF/lib/每个jar包
得到ClassLoader

先得到CLass，再得到ClassLoader
调用其getResourceAsStream();得到一个InputStream
相对当前.class文件所在目录
加/相对于classes下   

## 路径

**在web.xml中`<url-pattren>`路径**

Servlet路径
要么以"* "开头，要么以"/"开头

 **转发和包含路径**
以"/"开头，相对当前项目路径    

**重定向路径(客户端路径)**
以"/"开头，相对当前主机

**页面中超链接和表单路径**
与重定向相同，都是客户端路径，需要添加项目名

**ServletContext获取资源路径**
相对当前项目目录，即当前index.jsp所在目录

**ClassLoader获取资源路径**
相对classes目录

**Class获取资源路径**
以"/"开头相对classes目录
不以"/"开头，相对当前.class文件所在目录

## 编码

常见的字符编码：iso-8859-1（不支持中文）
gbk（系统默认编码，中国的国际码）
utf-8（万国码，支持全世界的编码）

***响应编码***

* 当使用respnse.getWrite()向客户端发送字符数据时，如果在之前没有设置编码，那么默认使用iso，因为iso不支持中文，一定乱码
* 在使用response.getWrite()之前使用response.setCharacterEncoding()来设置字符流的编码为gbk或utf-8，通常选择utf-8
* 在使用response.getWrite()之前使用response.setHeader("Content-type","text/html;charset=utf-8")来设置响应头，通知浏览器服务器这边使用的编码格式，并设置字符流编码
* 在getWrite()之前使用：
  * setHeader("Content-type","text/html;charset=utf-8")的快捷方法是：setContentType("text/html;charset=utf-8")

就不会乱码

***请求编码***
客户端发送给服务器的请求参数，在请求这个页面时，服务器响应的编码是什么，那么客户端发送请求时的编码就是什么
服务器端默认使用ISO-8859-1来解码
请求编码处理分为两种：

GET和POST：GET请求参数不在请求体中，而POST请求参数在请求体中，所以它们的处理方式是不同的

**GET请求编码处理：**

> String username =  new String(request.getParameter("iso-8859-1"),"utf-8");
>
> 在/cof/servler.xml中<Connector port中，URIEncoding=:UTF-8"/>配置URIEncoding=utf-8(不让用）

```java
String name = request.getParameter("name");
反编回来
byte[] bytes[] = name.getBytes("ISO-8859-1");
name = new String(bytes,"utf-8");
```

<u>URL最大长度2048，发送数据是URL一 部分，安全性较差</u>

**POST请求编码处理：**
String username = new String(request.getParameter("iso-8859-1"),"utf-8");
在获取参数之前调用request.setCharacterEncoding("utf-8");

**URL编码**

表单的类型：Content-Type:application/x-www-form-urlencoded，就是把中文转换成%后面跟随两位的16进制
在客户端和服务器之间传递中文时需要把它转换成网络适合的方式
它不是字符编码
它是用来在客户端与服务器之间传递参数用的一种方式
URL编码需要先指定一个字符编码，把字符串解码后，得到byte[]，然后把小于0的字节+256，再转换成16进制，前面再添加%
POST请求默认使用URL编码，tomcat会自动使用URL解码
URL编码：String username = URLEncoder.encode(username,"utf-8");
URL解码：String username = URLDecoder.decode(username,"utf-9");

## get和post的区别

1. get请求用来从服务器上获得资源，而post是用来向服务器提交数据；
2. get将表单中数据按照name=value的形式，添加到action 所指向的URL 后面，并且两者使用"?"连接，而各个变量之间使用"&"连接；post是将表单中的数据放在HTTP协议的请求头或消息体中，传递到action所指向URL；
3. get传输的数据要受到URL长度限制（1024字节）；而post可以传输大量的数据， POST数据是没有限制的，上传文件通常要使用post方式；
4. 使用get时参数会显示在地址栏上，如果这些数据不是敏感数据，那么可以使用get；对于敏感数据还是应用使用post；
5. get使用MIME类型application/x-www-form-urlencoded的URL编码（也叫百分号编码）文本的格式传递参数，保证被传送的参数由遵循规范的文本组成，例如一个空格的编码是"%20"。
6.  Jsp页面中的FORM标签里的method属性为get时调用doGet()，为post时调用doPost()。

## 在JS中==和===的区别？

****

简单来说： == 代表相同， ===代表严格相同,为啥这么说呢， 

这么理解： 当进行双等号比较时候：先检查两个操作数数据类型，如果相同， 则进行===比较， 如果不同， 则愿意为你进行一次类型转换， 转换成相同类型后再进行比较，而===比较时， 如果类型不同，直接就是false.

## 自动刷新,定时刷新

自动刷新不仅可以实现一段时间之后自动跳转到另一个页面，还可以实现一段时间之后自动刷新本页面。Servlet中通过HttpServletResponse对象设置Header属性实现自动刷新例如：

Response.setHeader("Refresh","1000;URL=http://localhost:8080/servlet/example.htm");

其中1000为时间，单位为毫秒。URL指定就是要跳转的页面（如果设置自己的路径，就会实现没过一秒自动刷新本页面一次）


推荐博文：

[Servlet(一)](https://www.cnblogs.com/xdp-gacl/p/3760336.html)

[Servlet(二)](https://www.cnblogs.com/xdp-gacl/p/3763559.html)

