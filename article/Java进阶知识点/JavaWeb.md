# JavaWeb



## 一、Servlet

#### 			关于系统架构

1. 系统架构包括什么形式？
   - C/S架构
   - B/S架构
2. 什么是C/S架构？
   - Client / Server（客户端 / 服务器）
   - C/S架构的软件或者说系统有哪些呢？
     - QQ
     - 微信
     - 只要需要安装客户端软件的都是C/S架构
   - C/S架构的特点：需要安装特定的客户端软件。
   - C/S架构的系统优点和缺点分别是什么？
     - 优点：
       - 速度快（软件中的数据大部分都是集成到客户端软件当中的，很少量的数据从服务器端传过来，所以C/S架构的系统速度快）
       - 体验好（速度快、界面炫酷）
       - 界面炫酷（专门的语言去实现界面的，更加灵活）
       - 服务器压力小（因为大量的数据都是集成在客户端软件中，所以服务器只需传送很少量的数据，所以服务器压力小）
       - 安全（因为大量数据都集成在客户端软件当中的，并且客户端有很多个，服务器虽然只有一个，但是就算服务器受损了，问题也不大，因为大量的数据在多个客户端上有缓存，有存储，所以从这个方面来说，C/S架构的系统比较安全）
     - 缺点：
       - 升级维护比较麻烦，成本高（每一个客户端软件都需要升级）
3. B/S架构
   - Browser / Server（浏览器 / 服务器）
     - ​	http://www.baidu.com
     - http://www.jd.com
   - B/S结构的系统是不是一个特殊的C/S系统？
     - 实际上B/S结构的系统还是一个C/S，只不过这个C比较特殊，这个Client是一个固定不变的浏览器软件。
   - B/S结构的系统优点和缺点分别是什么？
     - 优点：
       - 升级维护方便，成本比较低。（只需要升级服务器端即可）
       - 不需要安装特定的客户端软件，用户操作方便，只需打开浏览器，输入网址即可。
     - 缺点：
       - 速度慢（不是因为带宽低的问题，是因为所有的数据都是在服务器上，用户发送的每一个请求都是需要服务器全身心的响应数据，所以B/S结构的系统在网络中传送的数据量比较大）
       - 体验差（界面不是那么炫酷，因为浏览器只支持HTML CSS JavaScript，再加上速度慢）
       - 不安全（所有的数据都在服务器上，只要服务器发生火灾、地震等不可抗力，最终数据全部丢失）

------

#### 			B/S结构的系统通信原理

1. WEB系统的访问过程
   - 第一步：打开浏览器
   - 第二步：找到地址栏
   - 第三步：输入一个合法的网址
   - 第四步：回车
   - 第五步：在浏览器上会展示响应的结果
2. 关于域名：
   - https://www.baidu.com/（网址）
   - www.baidu.com（是一个域名）
   - 在浏览器地址栏上输入域名后，回车之后，域名解析器会将域名解析出来一个具体的IP地址和端口号等。
3. IP地址
   - 计算机在网络中的一个身份证号。在同一个网络中，IP地址是唯一的。
   - 有了IP地址才能建立连接。
4. 端口号
   - 一个端口代表一个软件，一个计算机当中有很多软件，每一个软件启动之后都有一个端口号。
   - 在同一个计算机上，端口号具有唯一性。
5. 什么是请求，什么是响应？
   - 请求和响应实际上说的是数据的流向不同。
   - 从Browser端发送数据到Servlet端，我们称为请求（request）。
   - 从Servlet端向Browser端发送数据，我们称为响应（response）。

------

#### 			Web服务器软件

1. WEB服务器软件有哪些？
   - Tomcat（WEB服务器）
   - jetty（WEB服务器）
   - JBOOS（应用服务器）
   - WebLogic（应用服务器）
   - WebSphere（应用服务器）
2. 应用服务器和WEB服务器的关系？
   - 应用服务器实现了JavaEE的所有规范。（JavaEE有13种不同的规范）
   - WEB服务器只实现了JavaEE中的Servlet + JSP两个核心的规范。
   - 所以应用服务器是包含WEB服务器的。
3. 关于Tomcat
   - tomcat：开源免费的轻量级WEB服务器。
   - tomcat还有另外一个名字：Catalina（美国的一个风景秀丽的岛屿）
   - tomcat的logo是一只公猫：寓意表示Tomcat服务器是轻巧的，小巧的，运行速度快。
   - tomcat是Java语言写的。
   - tomcat服务器想要运行，必须先有jre（Java的运行时环境）。
4. 关于tomcat服务器的目录
   - bin：这个目录是Tomcat服务器的命令文件存放的目录，比如：启动Tomcat，关闭Tomcat等。
   - conf：这个目录是Tomcat服务器的配置文件存放目录。（server.xml文件中可以配置端口号，默认Tomcat端口是8080）
   - lib：这个目录是Tomcat服务器的核心程序目录，因为Tomcat服务器是Java语言编写的，这里的jar包里面都是class文件。
   - logs：tomcat服务器的日志目录，tomcat服务器启动等信息都会在这个目录下生成日志文件。
   - temp：Tomcat服务器的临时目录，存储临时的文件。
   - webapps：这个目录当中就是用来存放大量的webapp（web application：web应用）。
   - work：这个目录是用来存放JSP文件翻译之后的Java文件以及编译之后的class文件。
5. 启动Tomcat
   - bin目录下有一个文件：startup.bat；通过它可以启动Tomcat服务器。
   - xxx.bat文件是什么文件？
      - bat文件是Windows操作系统专用的，bat文件是批处理文件，这种文件中可以编写大量的Windows的dos命令，然后执行bat文件就相当于批量执行dos命令。
   - startup.sh，这个文件在Windows当中无法执行，在Linux环境当中可以使用。在Linux环境下能够执行shell命令，大量的shell命令编写在shell文件当中，然后执行这个shell文件可以批量执行shell命令。
   - tomcat服务器提供了bat和sh文件，说明了tomcat服务器的通用性。
   - 分析startup.bat文件得出，执行这个命令，实际上最后是执行：catalina.bat文件。
   - catalina.bat文件中有这样一行配置：MAINCLASS=org.apache.catalina.startup.Bootstrap（这个类就是main方法所在的类）
   - tomcat服务器是Java语言编写的，所以启动tomcat服务器就是执行main方法。
   - 配置Tomcat服务器需要哪些环境变量？
      - JAVA_HOME （jdk的根目录）
      - CATALINA_HOME（tomcat服务器的根目录）
      - PATH（%JAVA_HOME%\bin 和 %CATALINA_HOME%\bin）
      - 启动Tomcat：startup.bat（可以省略.bat）
      - 关闭Tomcat：shutdown.bat（不可以省略.bat，因为shutdown与Windows的关机命令shutdown冲突，可以在tomcat目录下重命名shutdown.bat命令，例如：stop）
   - 测试Tomcat服务器是否启动成功
      - 打开浏览器，在浏览器的地址栏输入URL即可
         - http://ip地址:端口号
         - ip地址即本机地址：127.0.0.1，或者localhost。
         - 端口号：8080
         - 注意：必须要在执行startup的命令下测试，关闭了则不能弹出界面。
         - 关闭tomcat服务器最好是用命令关闭，不要直接关闭dos窗口。

------

#### 			实现一个最基本的web应用（就是一个纯html文件）

1. 第一步：找到CATALINA_HOME\webapps目录
   - 因为所有的webapp要放到webapps目录下。（如果不放到此目录下，Tomcat服务器找不到）
2. 第二步：在CATALINA_HOME\webapps目录下新建一个子目录名，例如：temp
3. 第三步：在temp目录下新建资源文件，例如：login.html
   - 编写login.html文件的内容
4. 第四步：启动tomcat服务器
5. 第五步：打开浏览器，在浏览器地址栏上输入URL：
   - http://127.0.0.1:8080/temp/login.html

------

#### 		一个合法的webapp目录结构

```
webapproot
	|-----WEB-INF
			|-----classes（存放字节码）
			|-----lib（第三方jar包）
			|-----web.xml（注册Servlet）
	|-----html
	|-----css
	|-----javascript
	|-----image
	.....
```

------

```
response.setContentType("text/html"); //设置响应的内容类型是普通文本或html代码
//需要在获取流对象之前设置有效
```

#### 		解决Tomcat服务器在DOS命令窗口中的乱码问题

将CATALINA_HOME/conf/logging.properties文件中的内容修改如下：

java.util.logging.ConsoleHandler.encoding = GBK（修改编码为GBK）

------

#### 		向浏览器响应一段HTML代码

```java
public void service(ServletRequest request,ServletResponse response){
	response.setContentType("text/html;charset=UTF-8");
	PrintWriter out = response.getWriter();
	out.print("<h1>hello servlet!</h1>")
}
```

------

#### 		在Servlet中链接数据库，怎么做？

1. Servlet是Java程序，所以在Servlet中完全可以编写JDBC代码连接数据库。
2. 在一个webapp中去连接数据库，需要将驱动jar包放到WEB-INF/lib目录下。

------

#### 		Servlet对象的生命周期

1. 什么是Servlet对象生命周期？             
   - Servlet对象什么时候被创建？
   - Servlet对象什么时候被销毁？
   - Servlet对象创建了几个？
   - Servlet对象的生命周期表示：一个Servlet对象从出生到最后的死亡，整个过程是怎样的。
2. Servlet对象是由谁来维护的？
   - Servlet对象的创建，对象上方法的调用，对象最终的销毁，Javaweb程序员是无权干预的。
   - Servlet对象的生命周期是由Tomcat服务器（WEB Server）全权负责的。
   - Tomcat服务器通常我们称为：WEB容器。（WEB Container）
   - WEB容器来管理Servlet对象的死活。
3. 我们自己new的Servlet对象受WEB容器的管理吗？
   - 我们自己new的Servlet对象是不受WEB容器管理的。
   - WEB容器创建的Servlet对象，这些Servlet对象都会被放到一个集合当中（HashMap），只有放到这个HashMap集合中的Servlet才能被WEB容器管理，自己new的Servlet对象不会被WEB容器管理。（自己new的Servlet对象不在容器当中）
   - web容器底层应该有一个HashMap这样的集合，在这个集合当中存储了Servlet对象和请求路径之间的关系。
4. 默认情况下，服务器在启动的时候Servlet对象并不会被实例化。（如果提前创建出来所有的Servlet对象，必然是耗费内存的，并且创建出来的Servlet如果一直没有用户访问，显然这个Servlet对象是一个垃圾，没必要创建）
5. 如果要Servlet启动的时候创建对象呢？
   - 在路径下加上<load-on-startup>0</load-on-startup>标签。中间写正整数（数字越小，优先级越高）（一般不写）
6. Servlet对象生命周期
   - 默认情况下服务器启动的时候对象并没有被实例化。
   - 当用户发送第一次请求的时候，Tomcat服务器马上调用了对象的init方法（init方法在执行的时候，对象已经存在了，已经被创建出来了）
   - 用户发送第一次请求的时候，init方法执行之后，Tomcat服务器马上调用对象的service方法。
   - 当用户发送第二次请求、第三次请求...的时候，Servlet对象并没有被新建，还是使用之前创建好的Servlet对象，直接调用该Servlet对象的service方法，这说明：
      - 第一：Servlet对象是单例的（单实例的，但是：Servlet对象是单实例的，但Servlet类并不符合单例模式，我们称之为假单例。之所以单例是因为Servlet对象的创建我们javaweb程序员管不着，这个对象创建只能是Tomcat说了算）
      - 第二：无参数构造方法、init方法只在用户第一次发送请求的时候执行。也就是说无参数构造方法只执行一次，init方法也只被Tomcat服务器调用一次。
      - 第三：只要用户发送一次请求：service方法必然会被Tomcat服务器调用一次。发送100次请求，service方法会被调用100次。
   - Servlet的destroy方法只被Tomcat服务器调用一次。
      - destroy方法是在什么时候调用的？
         - 在服务器关闭的时候
         - 因为服务器关闭的时候要销毁对象的内存。
         - 服务器在销毁对象内存之前，Tomcat服务器会自动调用该对象的destroy方法。
         - destroy方法执行的时候，对象还在，没有被销毁，destroy方法执行结束之后，对象的内存才会被Tomcat服务器释放。
   - 关于Servlet类中方法的调用次数：
      - 构造方法只执行一次
      - init方法只执行一次
      - service方法用户发送一次请求则执行一次
      - destroy方法只执行一次
7. ServletConfig
   - ServletConfig是什么？
      - javax.servlet.ServletConfig
      - 显然ServletConfig是Servlet规范中的一员
      - ServletConfig是一个接口（javax.servlet.Servlet也是一个接口）
   - 谁去实现这个接口？
      - web服务器
   - 总结：tomcat服务器实现了ServletConfig接口
   - 一个Servlet对象中有一个ServletConfig对象。100个Servlet，应该就有100个ServletConfig对象。（Servlet和ServletConfig对象是一对一）
   - ServletConfig对象是谁创建的？在什么时候创建？
      - tomcat服务器（web服务器）创建了ServletConfig对象
      - 在创建Servlet对象的时候，同时创建了ServletConfig对象

------

#### 		缓存机制有哪些？

1. 堆内存当中的字符串常量池。
   - “abc”先在字符串常量池中查找，如果有，则直接拿来用。没有则新建，再放入到字符串常量池中。
2. 堆内存中的整数型常量池。
   - [-128~127]一共256个Integer类型的引用，放在整数型常量池中。没有超出这个范围的话，直接从常量池中取。
3. 连接池（Connection Cache）
   - 这里说的连接池中的连接是Java语言连接数据库的连接对象：java.sql.Connection对象。
   - JVM是一个进程，MySQL也是一个进程。进程和进程之间建立连接，打开通道是很耗费资源的。所以可以先提前创建好N个Connection连接对象，将连接对象放到一个集合中，我们把这个放有Connection对象的集合称为连接池。每一次用户连接的时候不需要再新建连接对象了，省去了新建的环节，直接从连接池中获取连接对象，大大提升了访问效率。
   - 连接池
      - 最小连接数
      - 最大连接数
      - 连接池可以提升用户的访问效率，也可以保证数据库的安全性。
4. 线程池
   - Tomcat服务器本身就是支持多线程的。
   - Tomcat启动服务器的时候，会先创建好N个线程Thread对象，然后将线程对象放到集合中，称为线程池。用户发送请求过来之后，需要有一个对应的线程来处理这个请求，这个时候线程对象就会直接从线程池中拿，效率比较高。
5. redis
   - NoSQL数据库、非关系型数据库、缓存数据库。
   - 向ServletContext应用域中存储数据，也等于是将数据存放到缓存cache当中了。

------

#### 	HTTP协议

1. 什么是HTTP协议？

   - HTTP协议：是W3C制定的一种超文本传输协议

   - W3C：

      - 万维网联盟组织
      - 负责制定标准的：HTTP、HTML4.0、HTML5.0、XML、DOM等规范都是W3C制定的。
      - 万维网之父：蒂姆-伯纳斯-李

      

2. HTTP协议包括：

   - 请求协议：
      - 浏览器 向 服务器发送数据，叫做：请求（request）
      - 包括四部分：
         - 请求行
         - 请求头
         - 空白行
         - 请求体
   - 响应协议：
      - WEB服务器 向 浏览器发送数据，叫做：响应（response）
      - 包括四部分：
         - 状态行
         - 响应头
         - 空白行
         - 响应体
   - 请求行的三部分：
      - 第一部分：请求方式（7种）
         - get（常用）
         - post（常用）
         - delete
         - put
         - head
         - options
         - trace
      - 第二部分：URI
         - 什么是URI？统一资源标识符。代表网络中的某个资源的名字。但是通过URI是无法定位资源的。
         - 什么是URL？统一资源定位符。代表网络中的某个资源，同时，通过URL是可以定位到该资源的。
         - URI和URL是什么关系？有什么区别？
            - URL包括URI
            - http://localhost:8080/servlet/index.html 这是URL
            - /servlet/index.html 这是URI
      - 第三部分：协议版本号
   - 状态行分三部分：
      - 第一部分：协议版本号
      - 第二部分：状态码（HTTP协议中规定的响应状态号。不同的响应结果对应不同的号码）
         - 200表示请求响应成功，正常结束。
         - 404表示访问的资源不存在，通常是因为路径写错了，或者路径写对了，但是服务器对应的资源并没有启动成功。（404是前端错误）
         - 405表示前端发送的请求方式和后端请求的处理方式不一致时发生：
            - 比如：前端是POST请求，后端的处理方式按照GET方式进行处理，发生405
            - 比如：前端是GET请求，后端的处理方式按照POST方式进行处理，发生405
         - 500表示服务器端的程序出现了异常。一般会认为是服务器端的错误导致的。
      - 第三部分：状态的描述信息：
         - ok 表示正常成功结束
         - not found 表示资源找不到

3. 怎么向服务器发送GET请求，怎么向服务器发送POST请求？

   - 到目前为止，只有一种情况可以发送post请求：使用form表单，并且form标签中的method属性值为：method="post"。
   - 其它所有情况都是get请求：
      - 在浏览器地址栏上直接输入URL
      - 在浏览器上直接点击超链接
      - 使用form表单提交数据时，form标签中没有写method属性，默认就是get
      - ... ...

4. GET请求和POST请求的区别？

   - get请求发送数据的时候，数据会挂在URI的后面，并且在URI后面添加了一个 ？，？后面是数据。这样会导致发送的数据回显在浏览器的地址栏上。（get请求在 “请求行” 上发送数据）
   - post请求发送数据的时候，在请求体当中发送。不会回显到浏览器的地址栏上，也就是说post发送的数据，在浏览器上看不到。（post在 “请求体” 当中发送数据）
   - get请求只能发送到普通的字符串。并且发送的字符串长度有限制，不通的浏览器限制不同。
   - get请求无法发送大量数据。
   - post请求可以发送任何类型的数据，包括普通字符串，流媒体等信息：视频、声音、图片。
   - post请求可以发送大数据量，理论上没有长度限制。
   - get请求比较适合从服务器端获取数据。
   - post请求比较适合向服务器端上传数据。
   - get请求是安全的，因为get请求只是为了从服务器上获取数据，不会对服务器造成危险。
   - post请求是危险的，因为post请求是向服务器提交数据，如果这些数据通过后门的方式进入到服务器中，服务器是很危险的。另外post是为了提交数据，所以一般情况下拦截请求的时候，大部分会选择拦截（监听）post请求。
   - get请求支持缓存
      - 任何一个get请求最终的 “响应结果” 都会被浏览器缓存起来。
      - 一个get请求路径 对应 一个资源。
      - 实际上，只要发送get请求，浏览器做的第一件事都是先从本地浏览器缓存中找，找不到的时候才会去服务器上获取。这种缓存机制目的是为了提高用户的体验。
   - post请求不支持缓存
      - 因为post缓存没有意义。
   
5. GET请求和POST请求如何选择？什么时候用GET请求，什么时候用POST请求？

   - 怎么选择GET请求和POST请求呢？衡量标准是什么呢？你这个请求是想获取服务器端的数据，还是想从服务路上获取资源，建议使用GET请求，如果你这个请求是为了向服务器提交数据，建议使用POST请求。
   - 大部分的form表单提交，都是post方式，因为form表单中要填写大量的数据，这些数据是收集用户的信息，一般是需要传给服务器，服务器将这些数据保存/修改等。
   - 如果表单中有敏感信息，还是建议适用post请求，因为get请求会回显敏感信息到刘览器地址栏上。（例如：密码信息）
   - 做文件上传，一定是post请求。要传的数据不是普通文本。
   - 其他情况都可以使用get请求。
   - 不管你是get清求还是post浦求，发送的清求数据格式是完全相同的，只不过位置不同，格式都是统一的：
      - name=value&name=value&name=value&name=value
      - name是什么？
         -  以form表单为例：form表单中input标签的name。 

      - value是什么？
         -  以form表单为例：form表单中input标签的value。


------

##### 	模板方法设计模式

1. 什么是设计模式？
   - 某个问题的固定的解决方案。（可以被重复使用）
2. 有哪些设计模式？
   - GoF设计模式：
      - 通常我们所说的23种设计模式。（Gang of Four：4人组提出的设计模式）
      - 单例模式
      - 工厂模式
      - 代理模式
      - 门面模式
      - 责任链设计模式
      - 观察者模式
      - 模板方法设计模式
      - ....
   - JavaEE设计模式：
      - DAO
      - DTO
      - VO
      - pojo
      - ...
3. 什么是模板方法设计模式？
   - 在模板类的模板方法中定义核心算法骨架，具体的实现步骤可以延迟到子类当中完成。
4. 模板类通常是一个抽象类，模板类当中的模板方法定义核心算法，这个方法通常是final的（不是必须的，只是为了防止子类继承从而修改算法）
5. 模板类当中的抽象方法就是不确定实现的方法，这个不确定怎么实现的事交给子类去做。

------

#### 		HttpServlet源码分析

1. HttpServlet类是专门为HTTP协议准备的。比GenericServlet更加适合HTTP协议下的开发。

2. HttpServlet在哪个包下？

   - jakarta.servlet.http.HttpServlet

3. 到目前位置我们接触了servlet规范中的哪些接口？

   - jakarta.servlet.Servlet	                核心接口
   - jakarta.servlet.ServletConfig	     Servlet配置信息接口
   - jakarta.servlet.ServletContext       Servlet上下文接口
   - jakarta.servlet.ServletRequest      Servlet请求接口
   - jakarta.servlet.ServletResponse    Servlet响应接口
   - jakarta.servlet.ServletException    Servlet异常（类）
   - jakarta.servlet.GenericServlet        标准通用的Servlet类（抽象类）

4. HTTP包下都有哪些接口类和接口？jakarta.servlet.http.*;

   - jakarta.servlet.http.HttpServlet（HTTP协议专用的servlet类，抽象类）
   - jakarta.servlet.http.HttpServletRequest（HTTP协议专用的请求对象）
   - jakarta.servlet.http.HttpServletResponse（HTTP协议专用的响应对象）

5. HttpServletRequest对象中封装了什么信息？

   - HttpServletRequest，简称request对象。
   - HttpServletRequest中封装了请求协议的全部内容
   - Tomcat服务器（web服务器）将 “请求协议” 中的数据全部解析出来，然后将这些数据全部封装到request对象当中。也就是说只要面向HttpServlitRequest，就可以获取请求协议中的数据。

6. HttpServletResponse对象是专门用来响应HTTP协议到浏览器的。

7. HttpServletRequest接口中有哪些常用方法？

   - ```java
      //获取前端浏览器用户提交的数据：
      Map<String,String[]> getParameterMap();//这个是获取map
      Enumeration<String> getParameterNames();//这个是获取map集合中所有的key
      String[] getParameterValues(String name);//根据key获取map集合的value
      String getParameter(String name)//获取value这个一维数组当中的第一个元素。（最常用）
      //以上4个方法，和用户提交的数据有关系
       
          
      //eg：
      Map<String,String[]> parameterMap = request.getParameterMap();
      
      //通过key获取value
      String username = request.getParameter("username");
      String password = request.getParameter("password");
      //复选框时调用
      String[] interests = request.getParameterValues("interest");
      
      System.out.println(username);
      System.out.println(password);
      for(String interest : interests){
          System.out.println(interest);
      }
      ```

8. request对象实际上又称为 “请求域” 对象。

   - 应用域对象是什么？

      - ServletContext（Servlet上下文对象）

      - 什么情况下会考虑向ServletContext这个应用域当中绑定数据？

         - 第一：所有用户共享的数据。

         - 第二：这个共享的数据量很小。

         - 第三：这个共享的数据很少的修改操作。

         - 在以上三个条件满足的情况下，使用这个应用域对象，可以大大提高我们的执行效率。

         - 实际上向应用域中绑定数据，就相当于把数据放到了缓存（Cache）当中，然后用户访问的时候直接从缓存中取，减少IO操作，大大提升系统的性能，所以缓存技术是提高系统性能的重要手段。

         - ```java
            //ServletContext当中有三个操作域的方法：（四个域共享方法）
            void setAttribute(String name,Object obj);//向域当中绑定数据
            Object getAttribute(String name);//从域中根据name获取数据。
            void removeAttribute(String name);//将域当中绑定的数据移除
            ```

9. request和response对象的生命周期

   - request对象和response对象，一个是请求对象，一个是响应对象。这两个对象只在当前请求中有效。
   - 一次请求对应一个request。
   - N次请求则对应N个request。


------

#### 	关于转发

1. 跳转

   - 转发（一次请求）

      - ```java
         //第一步：获取请求转发器对象
         RequestDispatcher dispatcher = request.getRequesDispatcher("/b");
         //第二步：调用转发器的forward方法完成跳转/转发
         dispatcher.forward(request,response);
         
         //第一步和第二步联合：
         request.getRequestDispatcher("路径").forward(request,response);
         ```

2. 两个Servle怎么共享数据？

   - 将数据放到request域当中，然后AServlet转发到BServlet，保证AServlet和BServlet在同一次请求中，这样就可以做到两个Servlet，或者多个Servlet共享同一份数据。

3. 转发的下一个资源必须是一个Servlet吗？

   - 不一定，只要是Tomcat服务器当中的合法资源，都是可以转发的。例如：html...
   - 注意：转发的时候，路径的写法要注意，转发的路径以 "/" 开始，不加项目名。

4. 关于request对象中两个非常容易混淆的方法：

   - ```java
      //通过key获取value（获取请求域的值）
      String username = request.getParameter("username");
      
      //之前一定是执行过：request.setAttribute("name",new Object());
      //从request域中根据name获取数据
      Object obj = request.getAttribute("name");
      
      //以上两个方法的区别是什么？
      //第一个方法：获取的是用户在浏览器上提交的数据。
      //第二个方法：获取的是请求域当中绑定的数据。
      ```

5. HttpServletRequest接口的其它常用方法：

   - ```java
      //获取客户端的IP地址
      String remoteAddr = request.getRemoteAddr();
      
      //get请求在请求行上提交数据。
      //post请求在请求体上提交数据。
      //设置请求体的字符集。（这种方式不能解决get请求的乱码问题）
      //注意：tomcat10之后，request请求体当中的字符集默认就是utf-8，不需要设置字符集，不会出现乱码问题。
      request.setCharacterEncoding("utf-8");
      
      
      //在tomcat9之前（包括9），响应中文也是有乱码的，解决如下：
      response.serContentType("text/html;charset=UTF-8");
      //tomcat10不需要
      
      //动态获取用户根路径（使用较多）
      String contextPath = request.getContextPath();
      
      //获取请求方式
      String method = request.getMethod();
      
      //获取请求的URI
      String requestURI = request.getRequestURI();
      
      //获取servlet path（除去项目名的路径）
      String servletPath = request.getServletPath();
      ```


------

#### 	在一个web应用中应该如何完成资源的跳转

1. 在一个web应用中通过两种方式，可以完成资源的跳转：
   - 第一种：转发
   - 第二种：重定向
   
2. 转发和重定向有什么区别？
   - 代码上有什么区别？
   
      - 转发
   
         - ```java
            //获取请求转发器对象
            RequestDispatcher dispatcher = request.getRequestDispatcher("/dept/list");
            //调用请求转发器对象的forward方法完成转发
            dispatcher.forward(request,response);
            
            //合并代码
            request.getRequestDispatcher("/dept/list").forward(request,response);
            //转发的时候是一次请求，不管转发了多少次，都是一次请求。
            //AServlet转发到BServlet，再转发到CServlet，不管转发了多少次，都在同一个request当中。
            //因为调用forward方法的时候，会将当前的request和response对象传递给下一个Servlet。
            ```
   
      - 重定向
   
         - ```java
            //注意：路径上要加一个项目名，因为重定向是浏览器自主的发送一个全新的请求
            //只要是浏览器发送的请求，必须加项目名。
            response.sendRedirect("/oa/dept/list");
            ```
   
   - 形式上有什么区别？
   
      - 转发（一次请求）
         - 在浏览器地址栏上发送的请求是：http://localhost:8080/servlet03/a，最终请求结束后，浏览器地址栏上的地址还是这个，没变。
      - 重定向（两次请求）
         - 在浏览器地址栏上发送的请求是：http://localhost:8080/servlet/a，最终在浏览器地址栏上显示的地址是：http://localhost:8080/servlet/b
   
   - 转发和重定向的本质区别？
   
      - 转发：是由WEB服务器来控制的。A资源跳转到B资源，这个跳转动作是Tomcat服务器内部完成的。
      - 重定向：是浏览器完成的。具体跳转哪个资源，是浏览器说了算。
   
3. 转发和重定向应该如何选择？什么时候使用转发，什么时候使用重定向？

   - 如果上一个Servlet当中向request域当中绑定了数据，希望下一个Servlet当中把request域里面的数据取出来，使用转发机制。
   - 剩下的所有请求均使用重定向。（使用较多）


------

#### 	使用注解

1. 在Servlet类上使用：@WebServlet
2. @WebServlet注解中有哪些属性呢？
   - name属性：用来指定Servlet的名字。等同于：<servlet-name>
   - urlPatterns属性：用来指定Servlet的映射路径。可以指定多个字符串。<url-pattern>
   - loadOnStartUp属性：用来指定在服务器启动阶段是否加载该Servlet。等同于：<load-on-startup>
   - value属性：这个value属性和urlPatterns属性一致，都是用来指定Servlet的映射路径的。
   - 注意：
      - 不是必须将所有属性写上，只需提供需要的。
      - 当注解的属性是一个数组，并且数组中只有一个元素，花括号可以省略
      - 如果注解的属性名是value的话，属性名也可以省略
3. 注解对象的使用格式：
   - @注解名称（属性名=属性值，属性名=属性值，....）

------

## 	JSP

1. jsp实际上就是一个Servlet

   - index.jsp访问的时候，会自动翻译生成index jsp.java，会自动编译生成index jsp.class，那么index jsp这就是一个类。

   - 访问index.jsp，实际上执行的是index jsp.class中的方法。
   - index jps类继承HttpJspBase，而HttpJspBase类继承的是HttpServlet。所以index.jsp类就是一个Servlet类。
   - jsp的生命周期和Servlet生命周期完全相同。
   - jsp和servlet都是**假单例**的。

2. JSP是什么？

   - JSP是Java程序。（JSP本质还是一个Servlet）
   - JSP是：JavaServlet Pages的缩写。（基于Java语言实现的服务器端的页面）
   - Servlet是JavaEE的13个子规范之一，那么JSP也是JavaEE的13个子规范之一。
   - JSP是一套规范。所有的web容器/web服务器都是遵循这套规范的，都是按照这套规范进行的 “翻译”

3. 在jsp中指定编码格式：

   ```Java
   //表示响应的内容类型是text/html，采用的字符集是utf-8。
   <%@page contentType="text/html;charset=UTF-8" %>
   ```

4. 在jsp中编写Java程序

   ```java
   <% Java语句; %>  //写在方法区中的Java代码
       
   <%! %>  //写在类体中的Java代码（很少用,存在线程安全问题）
   ```

   - 这个符号当中编写的被视为Java程序，被翻译到Servlet类的service方法内部。
   - 要注意编写方法的规范。（和Java中编写方法一致）
   - 在service方法当中编写的代码是有顺序的，方法体当中的代码要遵循自上而下的顺序逐行执行。
   - 在同一个jsp中，<%%>可以出现多个。

5. JSP的专业注释

   ```jsp
   <%-- JSP的专业注释，不会被翻译到Java源代码当中。 --%>
   ```

6. JSP的输出语句

   ```jsp
   //向浏览器输出一个Java变量
   <% String name = "tzw"; out.write("name =" + name);%>
   //注意：以上代码中的out是JSP的九大内置对象之一。只能在service方法的内部使用。
   
   <%= %> //这个符号代表的是-->out.print();在方法体里输出
   
   //注意：<% %>里面不能再添加<% %>
   ```

7. JSP中out.write()和out.print()的区别：

   - out对象的类型是JspWrite。JspWrite继承了java.io.Write类。
   - print方法是子类JspWrite，write是Write类中定义的方法。
   - 重载的print方法可以将各种数据类型的数据转换成字符串的形式输出，而重载的write方法只能输出字符、字符数组和字符串等与字符相关的数据。
   - JspWrite类型的out对象使用print方法和write方法都能输出字符串，但是，如果字符串对象的值为null时，print方法将输出内容为“null”的字符串，而write方法则是抛出NullPointerException异常。

8. JSP本质上是一个Servlet，那么JSP和Servlet的区别是什么？

   - 职责不同
      - servlet的职责：收集数据。（Servlet的强项是逻辑处理，业务处理，然后连接数据库，获取 / 收集数据）
      - JSP的职责：展示数据。（JSP的强项是做数据的展示）

9. JSP的指令

   - 指令的作用：指导JSP的翻译引擎如何工作。（指导当前JSP翻译引擎如何翻译JSP文件）

   - 指令包括哪些？

      - include指令（基本不用）
      - taglib指令
      - page指令

   - 指令的使用语法

      - <%@指令名 属性名=属性值 属性名=属性值 属性名=属性值...%>

   - page指令中有哪些常用的属性？

      - ```
         <%@page session="true|false" %>
         true表示启用JSP的内置对象session，表示一定启动session对象。没有session对象则创建
         如果没有设置，默认值就是session="true"
         session="false"表示不启动内置对象session。当前JSP页面中无法使用内置对象session
         ```

      - ```
         <%@page contextType="text/json;charset=UTF-8" %>
         contextType属性用来设置响应的内容类型
         ```

      - ```
         <%@page pageEncoding=UTF-8 %>
         表示设置响应时采用的字符集
         ```

      - ```
         <%@page import="java.util.List,java.util.Date,java.util.ArrayList" %>
         import语句
         ```

      - ```
         <%@page errorpage="/error.jsp" %>
         当前页面出现异常之后，跳转到error.jsp页面
         ```

      - ```
         <%@page isErrorpage="true" %>
         表示启用JSP九大内置对象之一：exception
         打印异常信息：exception.printStackTrace(); //通常写在errorpage.jsp页面
         默认值是false
         ```

         

10. JSP的九大内置对象

   - jakarta.servlet.jsp.PageContext  pageContext	页面作用域

   - jakarta.servlet.http.HttpServletRequest  request   请求作用域

   - jakarta.servlet.http.HttpSession  session   会话作用域

   - jakarta.servlet.ServletContext  application   应用作用域

      - pageContext < request < session < application

      - 四个作用域都有：setAttribute、getAttribute、removeAttribute方法

      - 以上作用域使用原则：尽可能使用小的域

         

   - java.lang.Throwable  exception

      

   - jakarta.servlet.ServletConfig  config

      

   - java.lang.Object  page（就是this，当前的servlet对象）

      

   - jakarta.servlet.jsp.JspWriter  out（负责输出）

   - jakarta.servlet.http.HttpServletResponse  response（负责响应）


------

#### 	关于B/S结构系统的会话机制（session机制）

1. 什么是会话（session）？

   - 用户打开浏览器，进行一系列操作，然后最终将浏览器关闭，这个过程叫做：一次会话。
   - 会话在服务器端也有一个对应的Java对象，叫做：session。
   - 一个会话当中包含多次请求。
   - 在Java的servlet规范中，session对应的类名是：HttpSession（jakarta.servlet.http.HttpSession）
   - session机制实际上是一个规范，不同的语言对这种会话机制都有实现。
   - session对象最主要的作用是：保存会话状态。

2. 为什么需要session对象来保存会话状态？

   - 因为HTTP协议是一种无状态协议。
   - 什么是无状态？
      - 请求的时候，B和S是连接的，但是请求结束后，连接就断了。
      - 为什么要这样做？因为这样的无状态协议，可以降低服务器压力。
      - 只要B和S断开了，那么关闭浏览器这个动作，服务器是不知道的。

3. 为什么不使用request对象保存会话状态？为什么不使用ServletContext对象保存会话状态？

   - request.setAttribute()存，request.getAttribute()取，ServletContext也有这个方法。request是请求域，ServletContext是应用域。
   - request是一次请求一个对象。（点击一个超链接是一次请求）
   - ServletContext对象是服务器启动的时候创建，服务器关闭的时候销毁，这个ServletContext对象只有一个。（域太大）
   - request请求域（HttpServletRequest）、session会话域（HttpSession）、application域（ServletContext）
   - request < session < application
   - 他们三个域的公共方法：
      - setAttribute（向域中绑定数据）
      - getAttribute（从域当中获取数据）
      - removeAttribute（移除域当中的数据）
   - 使用原则：尽量使用小的域。

4. session对象的实现原理

   - HttpSession session = request.getSession();
   - 张三访问的时候获取的session对象就是张三的，李四访问的时候获取的session对象就是李四的。

5. session怎么获取？

   ```java
   //从服务器上获取当前的session对象，如果没有则新建
   HttpSession session = request.getSession();
   
   //从服务器上获取当前对象，如果获取不到则不会新建，返回null（相当于禁用session）
   HttpSession session = request.getSession(false);
   ```

6. session实现原理

   - JSESSIONID=xxxxx 这是以Cookie的形式保存在浏览器的内存中的。浏览器只要关闭，这个Cookle就没有了。
   - session列表是一个Map，map的key是sessionid，map的value是session对象。
   - 用户第一次请求，服务器生成session对象，同时生成id，将id发送给浏览器。
   - 用户第二次请求，自动将浏览器内存中的id发送给服务器，服务器根据id查找session对象。
   - 关闭浏览器，内存消失，cookie消失，sessionid消失，会话等同于结束。

7. 为什么关闭浏览器，会话结束？

   - 关闭浏览器之后，浏览器中保存的sessionId消失，下次重新打开浏览器之后，浏览器缓存中没有这个sessionId，自然找不到服务器中对应的session对象，session对象找不到等同于会话结束。

8. session什么时候被销毁？

   - 一种销毁：是超时销毁
   - 一种销毁：是手动销毁
      - session.invalidate();

9. Cookie禁用了，session还能找到吗？

   - cookie禁用是什么意思？服务器正常发送cookie给浏览器，但是浏览器不要了，拒收了，并不是服务器不发了。
   - 找不到了，每一次请求都会获取到新的session对象。
   - cookie禁用了，session机制还能实现吗？
      - 可以，需要使用URL重写机制。（在地址后面添加;jsessionid=12D1212xxxxxxxxx）
      - URL重写机制会提高开发者的成本。开发人员在编写任何请求路径的时候，后面都要添加一个sessionid，给开发带来了很大的难度，很大的成本。所以大部分网站禁用了cookie，就不能用了。

------

#### 	Cookie

1. session的实现原理中，每一个session对象都会关联一个sessionid，例如：
   - JSESSIONID=B1B9FBE8076BE4E01F414A8BE8056119
   - 以上这个键值对数据就是cookie对象。
   - 对于session关联的cookie来说，这个cookie是被保存在浏览器的 “运行内存” 当中。只要浏览器不关闭，用户再次发送请求的时候，会自动将运行内存中的cookie发送给服务器，例如，这个cookie：JSESSIONID=B1B9FBE8076BE4E01F414A8BE8056119就会再次发送给服务器。服务器就是根据这个值来找对应的session对象的。
2. cookie保存在什么地方？浏览器什么时候发送cookie，发送哪些cookie给服务器？
   - cookie最终是保存在浏览器客户端上的。
      - 可以保存在运行内存中（浏览器只要关闭cookie就消失了）
      - 也可以保存在硬盘文件中（永久保存）
   - 当第一次request的时候，服务器接收并创建cookie；用户第二次request的时候，浏览器发送请求并携带cookie一起发送给服务器。
   - 一个url对应多个cookie。（一对多）
3. cookie有什么用？
   - cookie和session机制都是为了保存会话状态
   - cookie是将会话状态保存在浏览器客户端上
   - session是将会话状态保存在服务器端上。（session对象是存储在服务器上）
4. 为什么要有cookie和session机制呢？
   - 因为http协议是无状态、无连接协议
5. cookie机制和session机制都不属于Java机制，实际上cookie机制和session机制都是HTTP协议的一部分。PHP开发中也有cookie和session机制，只要是做web开发，cookie和session机制都是需要的。
6. HTTP协议中规定：任何一个cookie都是由name和value组成的。name和value都是字符串类型的。
7. 在Java的servlet中，提供了一个Cookie类来专门表示cookie数据。jakarta.servlet.http.Cookie;
8. java程序怎么把cookie数据发送给浏览器？response.addCookie(cookie);
9. 在HTTP协议中是这样规定的：当浏览器发送请求的时候，会自动携带该path下的cookie数据给服务器。
10. 关于cookie的有效时间

   - 怎么用Java设置cookie的有效时间？

      - ```java
         cookie.setMaxAge(60*60);//设置cookie在一小时之后失效
         
         //如果设置有效时间为0，则表示cookie被删除。主要应用在删除浏览器上的同名cookie
         
         //设置cookie的有效时间 <0 ，表示该cookie不会被存储。（表示不会被存储在硬盘文件中，会放在浏览器运行内存当中。和不调用setMaxAge是同一效果）
         ```

   - 没有设置有效时间：默认保存在浏览器运行内存中，浏览器关闭则cookie消失。

   - 只要设置cookie的有效时间>0，这个cookie一定会存储到硬盘文件当中。

11. 设置cookie的关联路径方法：cookie.setPath(“路径名”)；

12. 关于cookie的path，cookie关联的路径：

    - 假设现在发送的请求路径是："http://localhost:8080/servlet/cookie/generate" 生成的cookie，如果cookie没有设置path，默认的path是什么？
       - 默认的path路径：http://localhost:8080/servlet/cookie 以及它的子路径
       - 也就是说，以后只要浏览器的请求路径是 http://localhost:8080/servlet/cookie 这个路径以及这个路径以下的子路径，cookie都会被发送到服务器。

13. 手动设置cookie的path

    ```java
    cookie.setPath("/servlet"); //表示只要是这个servlet项目的请求路径，都会提交这个cookie给服务器。
    ```

14. 浏览器发送cookie给服务器了，服务器中的Java程序怎么接收？

    ```java
    Cookie[] cookies = request.getCookies(); //这个方法可能返回null
    if(cookies != null){
        for(Cookie cookie : cookies){
            String name = cookie.getName();
            String name = cookie.getValue();
        }
    }
    ```

------

## EL表达式

1. EL表达式
   - Expression Language（表达式语言）
   - EL表达式可以代替JSP中的Java代码，让JSP文件中的程序看起来更加整洁、美观
   - EL表达式归属于JSP
   - EL表达式只能取，不能存。
   
2. EL表达式在JSP中的主要作用：
   - 从某个域中取出数据
   - 将取出的数据转换成字符串
   - 将字符串输出到浏览器
   
3. EL表达式基本的语法格式：
   - ${表达式}
   
4. EL表达式的使用：

   ```jsp
   <%
   	//创建user对象
   	User user = new User();
   	user.setUsername("mo-yu-jina");
   	user.setpassword("0826");
   	
   	//将User对象存储到某个域当中，因为EL表达式只能从某个范围中取数据
   	//数据是必须存储到四大域之中。
   	request.setAttritube("userObj",user);
   %>
   
   <%--使用EL表达式取--%>
   	${userObj}
   	等同于Java代码：<%=request.getAttritube("userObj")%>
   
   
   面试题：
   	${abc} 和 ${"abc"}的区别是什么？
   		${abc}：表示从某个域中取出数据，并且被取出的这个数据的name是“abc“，之前一定有这样的代码：域.setAttribute("abc",对象);
   		${"abc"}：表示直接将"abc"当作普通字符串输出到浏览器。不会从某个域中取数据。
   
   
   ${userObj}底层：
   	从域中取数据，取出user对象，然后调用user对象的toString方法，转换成字符串，输出到浏览器。
   <%--如果想输出对象的属性值，怎么办？--%>
   	${userObj.username}
       ${userObj.password}
   使用EL取出数据的前提是属性有get()方法。
   如果没有get()方法则报异常。报500错误。
   
   
   EL还有一种取数据的方式：（当name中有特殊符号（比如"."）时使用这种方式）
   	${userObj["username"]}
   取user的username，注意[]当中的需要加双引号
   如果[]里面没有加双引号的话，会将其看作变量。加了双引号，则去找user对象的username属性。
   
   
   <%--在没有指定范围的前提下，EL表达式优先从小范围中取数据--%>
   
   在EL表达式中可以指定范围来读取数据
   EL表达式中有4个隐含的隐式的范围对象
   pageScope requestScope sessionScope applicationScope
   <%--在同名的情况下取出不同域中的数据--%>
   ${pageScope.data}
   ${requestScope.data}
   ${sessionScope.data}
   ${application.data}
   
   
   数组和集合都是用下标取出数据：
   	${myList} //调用List集合的toString方法
   	${myList[0]} //求出第一个数据
   	${myList[1]} //取出第二个数据
       ...以此类推....
   注意：set集合没有下标。
   ```

5. 忽略EL表达式：

   - <%@page isELIgnored="true" %>  //这是全局控制

   - 如果是false，则表示不忽略EL表达式（默认值）

   - 可以使用反斜杠进行局部控制：

      ```
      \${username} 这样也可以忽略EL表达式
      ```

6. 使用EL表达式获取应用的根路径

   - ${pageContext.request.contextPath}

7. EL表达式的常用隐式对象：

   - pageContext

      ```
      应用的根路径：${pageContext.request.contextPath}
      ```

   - param

      ```
      爱好：${param.aihao} //获取的是请求参数一维数组当中的第一个元素
      ```

   - paramValues

      ```
      爱好：${paramValues.aihao[0],paramValues.aihao[1],paramValues.aihao[2]} 
      //获取数组中的元素
      ```

   - initParam

8. EL运算符：

   - 在EL表达式中，"+"运算符只能做求和运算，不会进行字符串拼接操作。当两边不是数字的时候，一定会转换成数字，转不成数组就报错。NumberFormatException。
   - EL表达式当中的 "==" 调用了重写的equals方法。（EL中还有一个运算符 eq ，和这个一样）
   - ${empty param.username}  判断是否为空


------

## JSTL标签库

1. 什么式JSTL标签库？
   - Java Standard Tag Lib（Java标准的标签库）
   - JSTL标签库通常结合EL表达式一起使用，目的式让JSP中的Java代码消失。
   - 标签是写在JSP中的，但实际上最终还是要执行对应的Java程序。（Java程序在jar包中）
   
2. JSTL的核心标签库

   ```
   <%@taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
   ```

3. JSTL标签的原理

   ```
   <%@taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
   以上uri后面的路径实际上指向了一个xxx.tld文件。
   tld文件实际上是一个xml配置文件。
   在tld文件中描述了“标签”和“Java类”之间的关系。
   以上核心标签库对应的tld文件是：c.tld文件。
   它在jakarta.servlet.jsp.jstl-2.0.0.jar里面META-INF目录下，有一个c.tld文件。
   ```

4. 配置文件tld解析

   ```
   <tag>
   	<description>对该标签的描述</description>
   	<name>catch</name> //标签的名字
   	<tag-class>org.apache.taglibs.standard.tag.common.core.CatchTag</tag-class> //标签对应的Java类
   	<body-content>JSP</body-content> //标签体当中可以出现的内容，如果是JSP，就表示标签体中可以出现符合JSP所有语法的代码。例如EL表达式。
   	<attribute>
   		<description>
   			对这个属性的描述
   		</description>
   		<name>var</name> //属性名
   		<required>false</required> //false表示该属性不是必须的。true表示该属性是必须的。
   		<rtexprvalue>false</rtexprvalue> //这个描述说明了该属性是否支持EL表达式。false表示不支持，true表示支持。
   	</attribute>
   </tag>
   
   <c:catch var="">
   	JSP...
   </c:catch>
   ```

   

------

## Filter过滤器

1. Filter是什么，有什么用，执行原理是什么？

   - Filter是过滤器
   - Fiter可以写在Servlet这个目标程序执行之前添加代码。也可以在目标Servlet执之后添加代码。之前之后都可以添加过滤规则。
   - 一般情况下，都是在过滤器当中编写公共代码。

2. 过滤器的写法：

   - 第一步：编写一个Java类实现一个接口：jakarta.servlet.Filter。并且实现这个接口中的所有方法。

      - init方法：在Filter对象第一次被创建之后调用，并且只调用一次。
      - doFilter方法：只要用户发送一次请求，则执行一次。发送N次请求，则执行N次。在这个方法中编写过滤规则。
      - destroy方法：在Filter对象被释放/销毁之前调用，并且只调用一次。

   - 第二步：在web.xml文件中对Filter进行配置。

      ```
      <filter>
      	<filter-name>filter2</filter-name>
      	<filter-class>com.myself.javaweb.servlet.Filter2</filter-class>
      </filter>
      <filter-mapping>
      	<filter-name>filter2</filter-name>
      	<url-pattern>*.do</url-pattern>
      </filter-mapping>
      ```

      ```
      或者使用注解：
      	@WebFilter({"*.do"})   //不推荐使用注解，因为后续更改过滤器执行顺序不方便，会修改源代码
      ```

3. 注意：

   - Servlet对象默认情况下，在服务器启动的时候是不会新建对象的。
   - Filter对象默认情况下，在服务器启动的时候会新建对象。
   - Servlet是单例的，Filter也是单例的。

4. 目标Servlet是否执行，取决于两个条件：

   - 第一：在过滤器当中是否编写了：chain.doFilter(request,response);代码。
   - 第二：用户发送的请求路径是否和Servlet的请求路径一致。

5. chain.doFilter(request,response);这行代码的作用：

   - 执行下一个过滤器，如果下面没有过滤器了，执行最终的Servlet。

6. 注意：Filter的优先级，天生的就比Servlet高。

   - /a.do对应一个Filter，也对应一个Servlet。那么一定是先执行Filter，然后再执行Servlet。

7. 关于Filter的配置路径：

   - /a.do、/b.do、/dept/save。这些配置方式都是精确匹配。
   - /* 匹配所有路径。
   - *.do 后缀匹配。（不要以 / 开始）
   - /dept/* 前缀匹配。

8. 在web.xml文件中进行配置的时候，Filter的执行顺序：

   - 依靠filter-mapping标签的匹配位置，越靠上优先级越高。

9. 过滤器的调用顺序，遵循栈数据结构（先进后出，后进先出）。

10. 使用@WebFilter的时候，Filter的执行顺序是怎么样的？

    - 执行顺序是：比较Filter这个类名。
    - 比如：
       - FilterA和FilterB，则先执行FilterA。
       - Filter1和Filter2，则先执行Filter1。

11. Filter的生命周期？

    - 和Servlet对象的生命周期一致。
    - 唯一的区别：Filter默认情况下，在服务器启动阶段就实例化，Servlet不会。

12. Filter过滤器这里有一个设计模式：

    - 责任链设计模式。
    - 过滤器最大的优点：
       - 在程序编译阶段不会确定调用顺序。因为Filter的调用顺序是配置到web.xml文件中的，只要修改web.xml配置文件中filter-mapping的顺序就可以调整Filter的执行顺序。显然Filter的执行顺序是在程序运行阶段动态组合的。那么这种设计模式被称为责任链设计模式。

------

## Listener监听器

1. 什么是监听器？

   - 监听器是Servlet规范中的一员。就像Filter一样。Filter也是Servlet规范中的一员。
   - 在Servlet中，所有的监听器接口都是以"Listener"结尾。

2. 监听器有什么用？

   - 监听器实际上是Servlet规范留给我们JavaWeb程序员的特殊时机。
   - 特殊的时刻如果想执行这段代码，就需要使用对应的监听器。

3. Servlet规范中提供了哪些监听器？

   - jakar.servlet包下：
      - ServletContextListener
      - ServletContextAttributeListener
      - ServletRequestListener
      - ServletRequestAttributeListener
   - jakarta.servlet.http包下：
      - HttpSessionListener
      - HttpSessionAttributeListener
         - 该监听器需要使用@WebListener注解进行标注。
         - 该监听器监听的是什么？是session域中数据的变化。只要数据变化，则执行相应的方法。主要检测点在session域对象上。
      - HttpSessionBindingListener
         - 该监听器不需要使用@WebListener进行标注
         - 假设User类实现了该监听器，那么User对象在被放入session的时候触发bind事件，User对象从session中删除的时候，触发unbind事件。
         - 假设Customer类没有实现该监听器，那么Customer对象放入session或者从session删除的时候，不会触发bind和unbind事件。
      - HttpSessionIdListener
         - session的id发生改变的时候，监听器中的唯一一个方法就会被调用。
      - HttpSessionActivationListener
         - 监听session对象的钝化和活化的。
         - 钝化：session对象从内存存储到硬盘文件。
         - 活化：从硬盘文件把session恢复到内存。

4. 实现一个监听器的步骤：以ServletContextListener为例。

   - 第一步：编写一个类实现ServletContextListener接口。并且实现里面的方法。

      ```
      void contextInitialized(ServletContextEvent event)
      void contextDestroyed(ServletContextEvent event)
      ```

   - 第二步：在web.xml文件中对ServletContextListener进行配置：

      ```
      <listener>
      	<listener-class>文件路径</listener-class>
      </listener>
      ```

      ```
      当然，第二步也可以不适用配置文件，可以直接用注解：
      	@WebListener
      ```

5. 注意：所有监听器中的方法都是不需要javaweb程序员调用的，由服务器来负责调用，什么时候调用呢？

   - 当某个特殊的事件发生（特殊的事件发生其实就是某个时机到了）之后，被web服务器自动调用。

