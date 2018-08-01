#web开发常见术语
##1.DNS：Domain Name System，域名系统<br>
万维网上作为域名和IP地址相互映射的一个分布式数据库，能够使用户更方便的访问互联网，而不用去记住能够被机器直接读取的IP数串。工作原理如下（以谷歌www.google.com）<br>
![avator](/Users/liyan/Desktop/3.1.dns_hierachy.png)
##2.TCP：Transmission Control Protocol传输控制协议<br>
是一种面向连接的、可靠的、基于字节流的传输层通信协议，由IETF的RFC 793定义。
##3.URL:Uniform Resource Locator，统一资源定位符<br>
用于描述一个网络上的资源。基本格式如下<br>
```
scheme://host[:port#]/path/.../[?query-string][#anchor]
scheme         指定底层使用的协议(例如：http, https, ftp)
host           HTTP服务器的IP地址或者域名
port#          HTTP服务器的默认端口是80，这种情况下端口号可以省略。如果使用了别的端口，必须指明，例如 http://www.cnblogs.com:8080/
path           访问资源的路径
query-string   发送给http服务器的数据
anchor         锚
```

##4.Cookie机制<br>
Web程序引入了Cookie机制来维护HTTP协议连接的可持续状态。
##5.HTTP协议<br>
HTTP是一种让Web服务器与浏览器(客户端)通过Internet发送与接收数据的协议,它建立在TCP协议之上，一般采用TCP的80端口。它是一个请求、响应协议--客户端发出一个请求，服务器响应这个请求。在HTTP中，客户端总是通过建立一个连接与发送一个HTTP请求来发起一个事务。服务器不能主动去与客户端联系，也不能给客户端发出一个回调连接。客户端与服务器端都可以提前中断一个连接。例如，当浏览器下载一个文件时，你可以通过点击“停止”键来中断文件的下载，关闭与服务器的HTTP连接。
##6.GET请求和POST请求的区别<br>
GET请求把参数包含在URL中，POST通过request body传递参数。HTTP是基于TCP/IP的关于数据如何在万维网中如何通讯的协议。HTTP的底层是TCP/IP，GET和POST的底层也是TCP/IP，也就是说GET和POST都是TCP链接。<br>

在万维网的世界中，TCP就像是汽车，TCP用来传输数据；HTTP是交通规则，HTTP给汽车运输设定了好几个服务类别，即GET、POST、PUT和DELETE等。HTTP只是个行为准则，而TCP才是GET和POST怎么实现的基本。<br>

不同的浏览器(发起http请求)和服务器(接受http请求)就是不同的运输公司。数据量太大对浏览器和服务器都是很大的负担。大多数浏览器都会限制URL的长度在2K字节，而大多数服务器最多处理64K大小的URL。超过的部分不处理。<br>

GET和POST本质上就是TCP链接，并无差别。但是由于HTTP的规定和浏览器/服务器的限制，导致他们在应用过程中体现出一些不同。<br>

GET产生一个TCP数据包；POST产生两个TCP数据包。<br>


