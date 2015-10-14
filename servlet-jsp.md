# Servlet 与 JSP

# JSP 与 SERVLET 的关系

综述：Java Servlet 是 JSP 技术的基础，而且大型的 Web 应用程序的开发需要 Java Servlet 和 JSP 配合才能完成。现在许多 Web 服务器都支持 Servlet，即使不直接支持 Servlet 的 Web 服务器，也可以通过附件的应用服务器和模块来支持 Servlet，这得益于 Java 的跨平台特性。另外，由于 Servlet 内部以线程方式提供提供服务，不必对于每个请求都启动一个进程，并且利用多线程机制可以同时为多个请求服务，因此 Servlet 的效率非常高。

但它并不是没有缺点，和传统的 CGI、ISAPI、NSAPI 方式相同，Java Servlet 也是利用输出 HTML 语句来实现动态网页的，如果用它来开发整个网站，动态部分和静态页面的整合过程将变得无法想象。这就是 SUN 还要推出 JSP 的原因。

如何正确理解 servlet？

servlet 的基本概念

一、Servlet 的结构

在具体掌握 servlet 之前，须对 Java 语言有所了解。我们假设读者已经具备一定的 Java 基础。在 Servlet API 中最重要的是 Servlet 接口（interface），所有的 servlets 都必须实现该接口，途径有很多：一是直接实现该接口，二是通过扩展类(class)来实现，如  HttpServlet。 这个 Servlet 接口提供了 servlet 与客户端联系的方法。Servlet 编写者可以在他们开发 servlet 程序时提供更多一些或所有的这样方法。

当一个 servlet 接收来自客户端的调用请求, 它接收两个对象：一个是 ServletRequest，另外一个是 ServletResponse。这个 ServletRequest 类概括从客户端到服务器之间的联系，而  ServletResponse 类概括从 servlet 返回客户端的联系。

ServletRequest 接口可以获取到这样一些信息，如由客户端传送的阐述名称，客户端正在使用的协议，产生请求并且接收请求的服务器远端主机名。它也提供获取数据流的 ServletInputStream, 这些数据是客户端引用中使用 HTTP POST 和 PUT 方法递交的。一个 ServletRequest 的子类可以让 servlet 获取更多的协议特性数据。例如： HttpServletRequest 包含获取 HTTP-specific 头部信息的方法。

ServletResponse 接口给出相应客户端的 servlet 方法。它允许 servlet 设置内容长度和回应的 mime 类型，并且提供输出流 ServletOutputStream，通过编写者可以发回相应的数据。 ServletResponse 子类可以给出更多 protocol- specific 内容的信息。 例如：HttpServletResponse 包含允许 servlet 操作 HTTP-specific 头部信息的方法。

上面有关类和接口的描述，构成了一个基本的 Servlet 框架。HTTP servlets 有一些附加的可以提供 session-tracking capabilities 的方法。servlet 编写者可以利用这些 API，在有他人操作时维护 servlet 与客户端之间的状态。

二、Servlet 的接口

我们编写的 Servlet ，一般从 Javax 包的 HttpServlet 类扩展而来，在 HttpServlet 中加入了一些附加的方法，这些方法可以被协助处理 HTTP 基本请求的 HttpServlet 类中的方法 service 自动地调用。这些方法有：

· doGet 用来处理 HTTP 的 GET 请求。

这个 GET 操作仅仅允许客户从 HTTP server 上取得（GET）资源。重载此方法的用户自动允许支持方法 HEAD。这个 GET 操作被认为是安全的，没有任何的负面影响，对用户来说是很可靠的。比如，大多数的正规查询都没有副作用。打算改变存储数据的请求必须用其他的 HTTP 方法。这些方法也必须是个安全的操作。方法 doGet 的缺省实现将返回一个 HTTP 的 BAD_REQUEST 错误。

方法 doGet 的格式：

```
protected void doGet(HttpServletResquest request, HttpServletResponse response)
throws ServletException,IOException;
```

· doPost 用来处理 HTTP 的 POST 请求。

这个 POST 操作包含了在必须通过此 servlet 执行的请求中的数据。由于它不能立即取得资源，故对于那些涉及到安全性的用户来说，通过 POST 请求操作会有一些副作用。

方法 doPost 的缺省实现将返回一个 HTTP 的 BAD_REQUEST 错误。当编写 servlet 时，为了支持 POST 操作必须在子类 HttpServlet 中实现（implement）此方法。

此方法的格式：

```
protected void doPost(HttpServletResquest request, HttpServletResponse response)
throws ServletException,IOException;
```

· doPut 用来处理 HTTP 的 PUT 请求。

此 PUT 操作模拟通过 FTP 发送一个文件。对于那些涉及到安全性的用户来说，通过 PUT 请求操作也会有一些副作用。

此方法的格式：

```
protected void doPut(HttpServletResquest request,HttpServletResponse response)
throws ServletException,IOException;
```

· doDelete 用来处理 HTTP 的 DELETE 请求。

此操作允许客户端请求一个从 server 移出的 URL。对于那些涉及到安全性的用户来说，通过 DELETE 请求操作会有一些副作用。

方法 doDelete 的缺省实现将返回一个 HTTP 的 BAD_REQUEST 错误。当编写 servlet 时，为了支持 DELETE 操作，必须在子类 HttpServlet 中实现（implement）此方法。

此方法的格式：

```
protected void doDelete (HttpServletResquest request, HttpServletResponse response) 
throws ServletException,IOException;
```
· doHead 用来处理 HTTP 的 HEAD 请求。

缺省地，它会在无条件的 GET 方法执行时运行，但是不返回任何数据到客户端。只返回包含内容信息的长度的 header。由于用到 GET 操作，此方法应该是很安全的（没有副作用）也是可重复使用的。此方法的缺省实现（implement）自动地处理了 HTTPDE 的 HEAD 操作并且不需要通过一个子类实现（implement）。

此方法的格式：

```
protected void doHead (HttpServletResquest request,HttpServletResponse response) 
throws ServletException,IOException;
```

· doOptions 用来处理 HTTP 的 OPTIONS 请求。

此操作自动地决定支持什么 HTTP 方法。比如说，如果读者创建 HttpServlet 的子类并重载方法 doGet，然后方法 doOptions 会返回下面的 header：

Allow：GET，HEAD，TRACE，OPTIONS

一般不需要重载方法 doOptions。

此方法的格式：

```
protected void doOptions (HttpServletResquest request, HttpServletResponse response)
throws ServletException,IOException;
```

· doTrace 用来处理 HTTP 的 TRACE 请求。

此方法的缺省实现产生一个包含所有在 trace 请求中的 header 的信息的应答（response）。在开发 servlet 时，多数情况下需要重载此方法。

此方法的格式：

```
protected void doTrace (HttpServletResquest request, HttpServletResponse response)
throws ServletException,IOException;
```

在开发以 HTTP 为基础的 servlet 中，Servlet 开发者关心方法 doGet 和方法 doPost 即可。

三、Servlet 的生命周期

如果读者写过 Java 的小应用程序（Applet）,那 Servlet 对你来说就不会太难，也许更为简单。因为 Servlet 不用考虑图形界面的应用。与小应用程序一样，Servlet 也有一个生命周期。Servlet 的生命周期是当服务器装载运行 servlets：接收来自客户端的多个请求并且返回数据给客户端，然后再删除移开 servlets。下面详细描述如下：

1．初始化时期
当一个服务器装载 servlet 时，它运行 servlet 的 init() 方法。

```
public void init(ServletConfig config) throws ServletException
{
super.init(); //一些初始化的操作，如数据库的连接
}
```

需要记住的是一定要在 init()结束时调用 super.init()。init()方法不能反复调用，一旦调用就是重装载 servlet。直到服务器调用 destroy 方法卸载 servlet 后才能再调用。

2．Servlet 的执行时期
在服务器装载初始化 servlet 后，servlet 就能够处理客户端的请求，我们可以用 service 方法来实现。每个客户端请求有它自己 service 方法：这些方法接收客户端请求，并且发回相应的响应。Servlets 能同时运行多个 service。这是很重要的，这样，service 方法可以按一个thread-safe 样式编写。如：service 方法更新 servlet 对象中的一个字段 field，这个字段是可以同时存取的。假如某个服务器不能同时并发运行 service 方法，也可以用SingleThreadModel 接口。这个接口保证不会有两个以上的线程（threads）并发运行。在 Servlet 执行期间其最多的应用是处理客户端的请求并产生一个网页。其代码如下：

```
PrintWriter out = response.getWriter();
out.println("＜html＞");
out.println("＜head＞＜title＞"# Servlet ＜/title＞＜/head＞");
out.println("＜body＞");
out.println("Hello World");
out.println("＜/body＞＜/html＞");
out.close();
```

3．Servlet 结束时期
Servlets 一直运行到他们被服务器卸载。在结束的时候需要收回在 init()方法中使用的资源，在 Servlet 中是通过 destory()方法来实现的。

```
public void destroy()
{
//回收在init()中启用的资源，如关闭数据库的连接等。
}
```

JSP 与 servlet 之间是怎样的关系？

JSP 主要关注于 HTML（或者 XML）与 Java 代码的结合，以及加入其中的 JSP 标记。如果一个支持 JSP 的服务器遇到一个 JSP 页面，它首先查看该页面是否被编译成为一个 servlet。由此可见，JSP 被编译成 servlet，即被转变为纯 Java，然后被装载入服务器执行。当然，这一过程，根据不同的 JSP 引擎而略有不同。

JSP 和 servlet 在应用上有什么区别

简单的说，SUN 首先发展出 SERVLET，其功能比较强劲，体系设计也很先进，只是，它输出 HTML 语句还是采用了老的 CGI 方式，是一句一句输出，所以，编写和修改 HTML 非常不方便。

后来 SUN 推出了类似于 ASP 的嵌套型的 JSP，把 JSP TAG 嵌套到 HTML 语句中，这样，就大大简化和方便了网页的设计和修改。新型的网络语言如 ASP，PHP 都是嵌套型的。

从网络三层结构的角度看，一个网络项目最少分三层：data layer，business layer,，presentation layer。当然也可以更复杂。

SERVLET 用来写 business layer 是很强大的，但是对于写 presentation layer 就很不方便。JSP 则主要是为了方便写 presentation layer 而设计的。当然也可以写 business layer。写惯了 ASP，PHP，CGI 的朋友，经常会不自觉的把 presentation layer 和 business layer 混在一起。比如把数据库处理信息放到 JSP 中，其实，它应该放在 business layer 中。

根据 SUN 自己的推荐，JSP 中应该仅仅存放与 presentation layer 有关的部分，也就是说，只放输出 HTML 网页的部份。而所有的数据计算、数据分析、数据库联结处理，统统是属于 business layer，应该放在 JAVA BEANS 中。通过 JSP 调用 JAVA BEANS，实现两层的整合。

实际上，微软前不久推出的 DNA 技术，简单说，就是 ASP+COM/DCOM 技术。与 JSP+BEANS 完全类似，所有的 presentation layer 由 ASP 完成，所有的 business layer 由 COM/DCOM 完成。通过调用，实现整合。

为什么要采用这些组件技术呢？因为单纯的 ASP/JSP 语言是非常低效率执行的，如果出现大量用户点击，纯 SCRIPT 语言很快就到达了他的功能上限，而组件技术就能大幅度提高功能上限，加快执行速度。

另外一方面，纯 SCRIPT 语言将 presentation layer 和 business layer 混在一起，造成修改不方便，并且代码不能重复利用。如果想修改一个地方，经常会牵涉到十几页 CODE，采用组件技术就只改组件就可以了。

综上所述，SERVLET 是一个不完善的产品，写 business layer 很好，写 presentation layer 就很逊色许多了，并且两层混杂。所以，推出 JSP+BAEN，用 JSP 写 presentation layer,用 BAEN 写 business layer。SUN 自己的意思也是将来用 JSP 替代 SERVLET。

所以，学了 JSP，不会用 JAVA BEAN 并进行整合，等于没学。

如何调用 servlet？

要调用 Servlet 或 Web 应用程序，请使用下列任一种方法：由 URL 调用、在<FORM>标记中调用、在<SERVLET>标记中调用、在 ASP 文件中调用。

1．由 URL 调用 Servlet

这里有两种用 Servlet 的 URL 从浏览器中调用该 Servlet 的方法：

（1）指定 Servlet 名称：当用 WebSphere 应用服务器管理器来将一个 Servlet 实例添加（注册）到服务器配置中时，必须指定"Servlet 名称"参数的值。例如，可以指定将 hi 作为 HelloWorldServlet 的 Servlet 名称。要调用该 Servlet，需打开 http: //your.server.name/servlet/hi。也可以指定 Servlet 和类使用同一名称（HelloWorldServlet）。在这种情况下，将由 http://your.server.name/servlet/ HelloWorldServlet 来调用 Servlet 的实例。

（2）指定 Servlet 别名：用 WebSphere 应用服务器 管理器来配置 Servlet 别名，该别名是用于调用 Servlet 的快捷 URL。快捷 URL 中不包括 Servlet 名称。

2．在<FORM>标记中指定 Servlet

可以在<FORM>标记中调用 Servlet。HTM 格式使用户能在 Web 页面（即从浏览器）上输入数据，并向 Servlet 提交数据。例如：

```
<FORM METHOD="GET" ACTION="/servlet/myservlet">
<OL>
<INPUT TYPE="radio" NAME="broadcast" VALUE="am">AM<BR>
<INPUT TYPE="radio" NAME="broadcast" VALUE="fm">FM<BR>
</OL>
（用于放置文本输入区域的标记、按钮和其它的提示符。）
</FORM>
```

ACTION 特性表明了用于调用 Servlet 的 URL。关于 METHOD 的特性，如果用户输入的信息是通过 GET 方法向 Servlet 提交的，则 Servlet 必须优先使用 doGet()方法。反之，如果用户输入的信息是通过 POST 方法向 Servlet 提交的，则 Servlet 必须优先使用 doPost()方法。使用 GET 方法时，用户提供的信息是查询字符串表示的 URL 编码。无需对 URL 进行编码，因为这是由表单完成的。然后 URL 编码的查询字符串被附加到 Servlet URL 中，则整个 URL 提交完成。URL 编码的查询字符串将根据用户同可视部件之间的交互操作，将用户所选的值同可视部件的名称进行配对。例如，考虑前面的 HTML 代码段将用于显示按钮（标记为 AM 和 FM），如果用户选择 FM 按钮，则查询字符串将包含 name=value 的配对操作为 broadcast= fm。因为在这种情况下，Servlet 将响应 HTTP 请求，因此 Servlet 应基于 HttpServlet 类。Servlet 应根据提交给它的查询字符串中的用户信息使用的 GET 或 POST 方法，而相应地使用 doGet() 或  doPost() 方法。

3．在<SERVLET>标记中指定 Servlet

当使用<SERVLET>标记来调用 Servlet 时，如同使用<FORM>标记一样，无需创建一个完整的 HTML 页面。作为替代，Servlet 的输出仅是 HTML 页面的一部分，且被动态嵌入到原始 HTML 页面中的其它静态文本中。所有这些都发生在服务器上，且发送给用户的仅是结果 HTML 页面。建议在 Java 服务器页面（JSP）文件中使用 <SERVLET> 标记。

原始 HTML 页面中包含<SERVLET> 和</SERVLET>标记。Servlet 将在这两个标记中被调用，且 Servlet 的响应将覆盖这两个标记间的所有东西和标记本身。如果用户的浏览器可以看到HTML源文件，则用户将看不到<SERVLET>和</SERVLET>标记。要在 Domino Go Webserver 上使用该方法，请启用服务器上的服务器端包括功能。部分启用过程将会涉及到添加特殊文件类型 SHTML。当 Web 服务器接收到一个扩展名为 SHTML 的 Web 页面请求时，它将搜索 <SERVLET> 和 </SERVLET>标记。对于所有支持的 Web 服务器，WebSphere 应用服务器将处理 SERVLET 标记间的所有信息。下列 HTML 代码段显示了如何使用该技术。

```
<SERVLET NAME="myservlet" CODE="myservlet.class" CODEBASE="url" initparm1= "value">
<PARAM NAME="parm1" VALUE="value">
</SERVLET>
```

使用 NAME 和 CODE 属性带来了使用上的灵活性。可以只使用其中一个属性，也可以同时使用两个属性。NAME 属性指定了 Servlet 的名称（使用 WebSphere 应用服务器管理器配置的），或不带.class 扩展名的 Servlet 类名。CODE 属性指定了 Servlet 类名。使用 WebSphere 应用服务器时，建议指定 NAME 和 CODE，或当 NAME 指定了 Servlet 名称时，仅指定 NAME。如果仅指定了 CODE，则会创建一个 NAME=CODE 的 Servlet 实例。装入的 Servlet 将假设 Servlet 名称与 NAME 属性中指定的名称匹配。然后，其它 SHTML 文件可以成功地使用 NAME 属性来指定 Servlet 的名称，并调用已装入的 Servlet。NAME 的值可以直接在要调用 Servlet 的 URL 中使用。如果 NAME 和 CODE 都存在，且 NAME 指定了一个现有 Servlet，则通常使用 NAME 中指定的 Servlet。由于 Servlet 创建了部分 HTML 文件，所以当创建 Servlet 时，将可能会使用 HttpServlet 的一个子类，并优先使用 doGet()方法（因为 GET 方法是提供信息给  Servlet 的缺省方法）。另一个选项是优先使用 service()方法。另外，CODEBASE 是可选的，它指定了装入 Servlet 的远程系统的 URL。请使用 WebSphere 应用服务器管理器来从 JAR 文件配置远程 Servlet 装入系统。

在上述的标记示例中，initparm1 是初始化参数名，value 是该参数的值。可以指定多个"名称-值"对的集合。利用 ServletConfig 对象（被传递到 Servlet 的 init()方法中）的 getInitParameterNames()和 getInitParameter()方法来查找参数名和参数值的字符串数组。在示例中，parm1 是参数名，并在初始化 Servlet 后被才被设置某个值。因为只能通过使用"请求"对象的方法来使用以<PARAM>标记设置的参数，所以服务器必须调用 Servlet service()方法，以从用户处传递请求。要获得有关用户的请求信息，请使用 getParameterNames()、getParameter() 和 getParameterValues()方法。

初始化参数是持续的。假设一台客户机通过调用一个包含某些初始化参数的 SHTML 文件来调用 Servlet。并假设第二台客户机通过调用第二个 SHTML 文件来调用同一个 Servlet，且该 SHTML 中未指定任何初始化参数。那么第一次调用 Servlet 时所设置的初始化参数将一直可用，并且通过所有其它 SHTML 文件而调用的所有后继 Servlet 都不会更改该参数。直到 Servlet 调用了 destroy()方法后，才能重新设置初始化参数。例如，如果另一个 SHTML 文件指定了另一个不同的初始化参数值，虽然已此时已装入了 Servlet，但该值仍将被忽略。

4．在 ASP 文件中调用 Servlet
如果在 Microsoft Internet Information Server（IIS）上有遗留的 ASP 文件，并且无法将 ASP 文件移植成 JSP 文件时，可用 ASP 文件来调用 Servlet。在 WebSphere 应用服务器中的 ASP 支持包括一个用于嵌入 Servlet 的 ActiveX 控制，下面介绍 ActiveX 控制 AspToServlet 的方法和属性。

该方法说明如下：

（1）String ExecServletToString(String servletName)；执行 ServletName，并将其输出返回到一个字符串中。

（2）ExecServlet(String servletName)；执行 ServletName，并将其输出直接发送至 HTML 页面。

（3）String VarValue(String varName)；获得一预置变量值（其它格式）。

（4）VarValue(String varName, String newVal)；设置变量值。变量占据的总大小应小于0.5个千字节（Kbyte）。且仅对配置文件使用这些变量。

其属性如下：

= Boolean WriteHeaders；若该属性为真，则 Servlet 提供的标题被写入用户处。缺省值为假。
= Boolean OnTest；若该属性为真，服务器会将消息记录到生成的 HTML 页面中。缺省值为假。
下列 ASP 脚本示例是以 Microsoft Visual Basic Scripting（VBScript）书写的。

```
<%
' Small sample asp file to show the capabilities of the servlets and the ASP GateWay ...
%>
<H1> Starting the ASP->Java Servlet demo</H1>
<%
' Create a Servlet gateway object and initialize it ...
Set Javaasp = Server.CreateObject("AspToServlet.AspToServlet")
' Setting these properties is only for the sake of demo.
' These are the default values ...
Javaasp.OnTest = False
Javaasp.WriteHeaders = False
' Add several variables ...
Javaasp.VarValue("gal") = "lag"
Javaasp.VarValue("pico")= "ocip"
Javaasp.VarValue("tal") = "lat"
Javaasp.VarValue("paz") = "zap"
Javaasp.VarValue("variable name with spaces") = "variable value with spaces"
%>
<BR>
Lets check the variables
<%
Response.Write("variable gal = ")
Response.Write(Javaasp.VarValue("gal"))
%>
<BR>
<%
Response.Write("variable pico = " & Javaasp.VarValue("pico"))
%>

<BR>
<HR>
<%
galout = Javaasp.ExecServletToString("SnoopServlet")
If Javaasp.WriteHeaders = True Then
%>
Headers were written <%
Else
%>
Headers were not written <%
End If
Response.Write(galout)
%>
<H1> The End ...</H1>
```

如何设置 servlet 类的路径？

因为各个服务器对访问 servlet 的策略不尽相同，所以在设置 servlet 类路径时应该视情况而定。
对于开发中的 servlet，只需确认包含 Javax.servlet 的 JAR 文档在您的类路径中，并运用如Javac 的普通开发工具。
对于 JSDK：JSDK_HOME/servlet.jar
JSDK_HOME/server.jar
对于 Tomcat：TOMCAT_HOME/lib/servlet.jar
对于运行中的 servlet，必须为 servlet 引擎设置类路径，这根据不同的引擎，有不同的配置，如哪些库和目录应包括，哪些不应包括。注：对于 servlet 的动态加载引擎如 JRun, Apache Jserv, Tomcat，包含 servlet 类文件的目录不应在类路径中，而应在 config 文件中配置。否则，servlet 可以运行，但不能被动态再加载。

Servlet 2.2 规范认为以下应被容器自动包括，因此您不必把他们手工添加到类路径。

· 所有的类应放在 webapp/WEB-INF/classes 目录下

· 所有 JAR 文件放在 webapp/WEB-INF/lib 目录下

· 对 webapps 的应用体现在文档系统中，对已打包进 JAR 文档的 webapps 的应用应放入容器的 webapps 目录。（例如，TOMCAT_HOME/webapps/myapp.jar）

另外，由 Gene McKenna(mckenna@meangene.com)撰写的"The Complete CLASSPATH Guide for Servlets"详细叙述了如何为 JavaWebServer 和 Jrun 设置类路径。

如何实现 servlet 与 applet 的通信？

这个例子将向读者展示服务器端程序（Servlet）和小应用程序（Applet）之间是如何完成通信活动的。它由三个文件组成，一个是 sendApplet.Java 文件，用于实现 Applet，一个是 receiveservlet.Java，用于实现 servlet，还有一个是 add -servlet.html，用于调用 Applet。

在 sendApplet.Java 文件中，最重要的要属 init()函数和 Send()函数，其中 init()函数用来生成整个 Applet 的用户操作界面，包括消息文本框、发送按钮等等。而消息的发送过程则由 Send()函数来完成。请仔细阅读下面的代码：

```
private void Send()
{
message = sendText.getText();
//清除用户的输入信息
sendText.setText("");
showStatus("Message send!");
//把输入的字符串转化为 x-www-form-urlencoded 格式
String queryString = "/servlet/ReceiveServlet?message=" + URLEncoder.encode ( message ) ;
p("Attempting to send:"+message);

//建立与Servlet的联接，并取得Servelt的输出信息
try {
connect = (new URL(chatURL,queryString)).openConnection();
showStatus("open connection!");
//下次连接不用Cache
connect.setDefaultUseCaches(false);
//这次连接也不用Cache
connect.setUseCaches(false);
//打开淂流用于读数据
connect.setDoInput(true);
//不能用于写数据
connect.setDoOutput(false);
//服务器与客户的真正连接
connect.connect();
p("Made connection to "+connect);
showStatus("Open Stream!");
DataInputStream in = new DataInputStream(connect.getInputStream());
showStatus("reading!");
message = in.readLine();
while (message! = null)
{
//在消息文本框显示Servlet生成的信息
messageText.setText(message);
message = in.readLine();
}
}catch(MalformedURLException e2)
{
System.err.println("MalformedURLException!");
e2.printStackTrace(System.err);
showStatus("MalformedURLException!");
}catch(IOException e1)
{
System.err.println("IOException!");
e2.printStackTrace(System.err);
showStatus("IOException");
}
}
```

整个 Applet 的详细代码请见 sendApplet.Java。

当 Applet 与 Servlet 建立连接后，工作就可以交给 Servlet 了，由它来解析客户端的请求，获得参数 message 的值，然后将适当信息返回给客户端，并由 Applet 进行显示。完成该功能的是 receiveservlet.Java 中的 service()函数：

```
public void service (HttpServletRequest req,HttpServletResponse res)
throws ServletException,IOException
{
res.setContentType("text/plain");
ServletOutputStream out = res.getOutputStream();
out.print("receive user message:");
out.print(req.getParameter("message"));
}
```

该 Servlet 的详细源代码请见 receiveservlet.Java。
最后一个文件是 add-servlet.html，它用来调用 Applet：

```
<html>
<head>
<title>sendApplet</title>
</head>
<body>
<hr>
<applet code=sendApplet width=400 height=300 ></applet>
<hr>
</body>
</html>
```

如何应用应用 Servlet 进行图象处理？

我们在处理数据时，有时希望能用图象直观的表述，在这里有一个巧方法，能方便快捷的实现一些简单的图形（不能称之图象），比如条形图，我们不必去用 Java 来生成并显示图象，（Java 生成图象很慢），我们可以这样来作，先用作图工具作一个很小的你需要的图片，再根据你所处理的数据量来实时的加长它，就可以得到所要表述的图例。比如我们在数据库中得到了一组数据，我们从中找出最大的那一个，按比列设定其<img>标签的长度，其它的数据图形则可与它相比，得到<img>的长度，这样，一个简简单单的条形图就出来。但有时一些简单的图形已经不能解决我们实际遇到的情况，比如曲线图就不能用这种方法，这时我们需要生成 Java 图象，也许大家都用过 applet 这样的程序吧，若访问量不大，而实时性又很特殊时（比如股票系统），必须这样用它。但事实上，我们 web 程序大多有前后台之分，前台浏览，后台维护。这样我们可以在后台用 servlet 实时动态定时地生成图象文件，而前台只是查看静态图片，这比你用 applet 来动态产生图象的速度快了不知多少倍，因为 applet 来动态产生图象，有两个地方很费时，一是数据库查询时间，二是 applet 本身生成图象就很慢。下面以一个简单的例子来说明一下怎样生成并写入图象文件，本例注重的是怎样写入图象文件，相信写过 applet 的读者会生成更加漂亮的图象。

```
package test;
import Javax.servlet.*;
import Javax.servlet.http.*;
import Java.io.*;
import Java.util.*;
import Java.awt.image.BufferedImage;
import com.sun.image.codec.jpeg.*;
import Java.awt.image.*;
import Java.awt.*;

public class Servlet2 extends HttpServlet
{
public void init(ServletConfig config) throws ServletException {
super.init(config);
}

public void doGet(HttpServletRequest request, HttpServletResponse response)
throws ServletException, IOException
{
String sFileName = "e:/temp/name.jpg";
try{
FileOutputStream fos = new
FileOutputStream(sFileName);
BufferedImage myImage = new BufferedImage(225, 225,BufferedImage. TYPE_INT_RGB);
Graphics g = myImage.getGraphics();
g.setColor(Color.white);
g.fillRect(0,0,225,225);
g.setColor(Color.black);
g.drawString("Finance Balance Summary", 40, 15);
g.drawString("Primary", 90, 30);
g.setColor(Color.darkGray);
g.fillRect(15,193,7,7);
g.setColor(Color.black);
g.drawString("% Operating", 25, 200);
g.setColor(Color.yellow);
g.fillRect(130,193,7,7);
g.setColor(Color.black);
g.drawString("% Term", 140, 200);
g.setColor(Color.lightGray);
g.fillRect(15,213,7,7);
g.setColor(Color.black);
g.drawString("% Mortgage", 25, 220);
g.setColor(Color.green);
g.fillRect(130,213,7,7);
g.setColor(Color.black);
g.drawString("% Lease", 140, 220);
JPEGImageEncoder jpg = JPEGCodec.createJPEGEncoder(fos);
jpg.encode(myImage);
}catch (Exception e)
{
String exceptionThrown = e.toString();
String sourceOfException = " Method";
System.out.println("Origional Exception Thrown: " +exceptionThrown + '/r' + '/n');
System.out.println("Origional SourceOfException: " + sourceOfException +'/r' + '/n');
} // CatchStatementEnd
}
}
```

如何通过 Servlet 调用 JavaBean 输出结果集

以此我们通过一个例子进行说明，该例演示了如何通过 Servlet 调用 JavaBean 输出结果集，并打印的方法，共由两个文件组成，一个是 JavaBean，用于实现对数据库的访问，并获得结果集；另一个是 Servlet，主要负责 JavaBean 的调用，并将结果集发送到客户端。

在 JavaBean 中，我们将访问 DB2 样例数据库（sample）中的 STAFF 表，至于如何实现对数据库的访问，读者可以参考《JSP 与 JDBC》一章。此外，读者可以通过修改部分参数，来实现对其他数据库、表的访问，达到举一反三的效果。

该 JavaBean 的核心是 execute()函数：

```
public void execute()
{
try {
//装载JDBC驱动程序
Class.forName("COM.ibm.db2.jdbc.app.DB2Driver").newInstance();
//建立对数据库的连接
conn = DriverManager.getConnection("jdbc:db2:sample", "db2admin", "db2admin");
stmt = conn.createStatement();
String sql = "SELECT * FROM STAFF WHERE DEPT=20";
//执行查询语句，返回结果集
ResultSet rs = stmt.executeQuery(sql);
setResult(rs);
} catch (SQLException e) {
} catch (IllegalAccessException e2) {
} catch (ClassNotFoundException e3) {
} catch (InstantiationException e4) {}
}
```

JavaBean 的具体源代码请见 Tbean.Java。

知道数据是如何获取之后，下面我们来看一下Servlet 是如何来调用上述 JavaBean 的。

同样看 service()方法即可（详细源代码请见 Tservlet.Java）：

```
public void service(HttpServletRequest req, HttpServletResponse res)
throws ServletException, IOException
{
try {
//实例化JavaBean
Demo.TBean Javabean = new Demo.TBean();
Javabean.execute();
ResultSet rs1 = Javabean.getResult();
PrintWriter out = res.getWriter();
res.setContentType("text/html");
out.println("<table border=1>"=;
out.println("<H1>Hello World</H1>"=;
out.println("<td>ID</td><td>NAME</td><td>DEPT</td><td>JOB</td><td>YEARS</td><td>SALARY</td><td>COMM</td>"=;
while (rs1.next())
{
out.println("<tr>"=;
for (int i = 1; i <= 7; i++=
out.println("<td>" + rs1.getString(i) + "</td>"=;
out.println("</tr>"=;
}
out.println("</table>"=;
Javabean.Sqlclose();
} catch (SQLException e) {}
}
```

//运行：在 VisualAge for Java 的 IBM Websphere Test Environment 的环境下：
//http://localhost:8080/servlet/Demo.TServlet

如何用 Servlet 来中断涉及的多线程

现在我们已经知道，当服务器要卸载一个 Servlet 时，它会在所有的 service 都已经完成后再调用 destroy()方法。如果程序的操作运行需要很长时间，destroy()被调用时就可能还有其他线程在运行。Servlet 程序员必须保证所有的线程都已经完成。

长时间运行响应客户端请求的那些 Servlet 应当保留当前有多少方法在运行的记录。它的 long-running 方法应当周期性地轮流询问以确保它们能够继续运行下去。如果 Servlet 被 destroy()方法调用，那么这个 long-running 方法必须停止工作或清除。

举例，变量 serviceCounter 用来统计有多少 service 方法在运行，变量 shuttingDown 显示这个 Servlet 是否被 destroy。每个变量有它自己的获取方法：

```
public ShutdownExample extends HttpServlet
{
private int serviceCounter = 0;
private Boolean shuttingDown;
…
//serviceCounter
protected synchronized void enteringServiceMethod()
{
serviceCounter++;
}
protected synchronized void leavingServiceMethod()
{
serviceCounter--;
}
protected synchronized int numServices()
{
return serviceCounter;
}
//shuttingDown
protected setShuttingDown(Boolean flag)
{
shuttingDown = flag;
}
protected Boolean isShuttingDown()
{
return shuttingDown;
}
```

这个 service 方法每次在它进入时要增加，而在它返回退出时要减少：

```
protected void service(HttpServletRequest req , HttpServletResponse resp)
throws ServletException IOException
{
enteringServiceMethod();
try{
super.service(req , resp);
}
finally {leavingServiceMethod();}
}
```

destroy 方法应当检查 serviceCounter，如果存在长时间方式运行的话，设置变量 shuttingDown。这个变量将会让那个正在处理请求的线程知道该结束了。destroy 方法应当等待这几个 service 方法完成，这样就是一个清楚的关闭过程了。

```
public void destroy()
{
//检查是否有线程在运行，如果有，告诉它们停止
if (numServices() > 0)
{
setShuttingDown(true);
}
//等待它们停止
while(numService() > 0)
{
try{
thisThread.sleep(interval);
}catch(InterruptedException e) {}
}
}
```

long-running 方法如必要应当检查这个变量，并且解释它们的工作：

```
public void doPost(…)
{
…
for(i = 0; ((i < lotsOfStuffToDo) && !isShuttingDown()); i++)
{
try{
partOfLongRunningOperation(i);
}catch (InterruptedException e) {}
}
}
```
