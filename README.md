# tcp-ip-


是要学习学习这些网络通信的知识了


我想花三天时间简单的了解一下tcp/ip的有关知识应该差不多吧

#行吧，先来慢慢磨我对tcp/ip的理解吧


tcp/ip就是一个通俗的协议，其包括http协议，其基于ipv4属于第二代互联网技术




ip(我们居住小区的地址)，MAC地址（地址中那个房间的人），



tcp（就是安全的把东西带个对方）


dns，（就是一种对应关系吧，比如196.123.1.1，对应着www.weizhong.com，这就是dns，就是方便人记忆罢了，其和http协议差不多）


#tcp/IP协议分为四层


1，链路层，用来处理连接网络的硬件部分




2，网络层，处理在网络上流动的数据包，（数据包是网络传输的最小单位），就是在众多的路径中选择一条传输路线，ip协议


3，传输层，tcp(传输控制协议),udp（用户数据报协议，不可靠）




4,应用层，ftp（文件传输协议），dns（域名系统），http协议


以上可以参考http://www.cnblogs.com/roverliang/p/5176456.html



#下面说说Android下面的网络编程吧

基本知识，http（短连接），scoket（长连接）



#1，Scoket（嵌套字），socket就是一组调用接口（API），封装了做tcp/ip开发的网络接口，通过

Socket
，我们才能使用TCP/IP协议。




#2,tcp连接（三次握手）

第一次握手：客户端发送syn包(syn=j)到服务器，并进入SYN_SEND状态，等待服务器确认；

第二次握手：服务器收到syn包，必须确认客户的SYN（ack=j+1），同时自己也发送一个SYN包（syn=k），即

SYN+ACK包，此时服务器进入SYN_RECV状态； 

第三次握手：客户端收到服务器的SYN＋ACK包，向服务器发送确认包ACK(ack=k+1)，此包发送完毕，客户端

和服务器进入ESTABLISHED状态，完成三次握手。 

握手过程中传送的包里不包含数据，三次握手完毕后，客户端与服务器才正式开始传送数据。理想状态下，TCP

连接一旦建立，在通信双方中的任何一方主动关闭 连接之前，TCP 连接都将被一直保持下去。断开连接时服务

器和客户端均可以主动发起断开TCP连接的请求，断开过程需要经过“四次握手”。





#3，scoket连接

由于通常情况下Socket连接就是TCP连接，因此Socket连接一旦建立，通信双方即可开始相互发送数据内容，

直到双方连接断开。但在实际网络应用中，客户端到服务器之间的通信往往需要穿越多个中间节点，例如路由

器、网关、防火墙等，大部分防火墙默认会关闭长时间处于非活跃状态的连接而导致 Socket 连接断连，因此

需要通过轮询告诉网络，该连接处于活跃状态。

建立Socket连接至少需要一对套接字，其中一个运行于客户端，称为ClientSocket ，另一个运行于服务器

端，称为ServerSocket 。

套接字之间的连接过程分为三个步骤：服务器监听，客户端请求，连接确认。

1。服务器监听：服务器端套接字并不定位具体的客户端套接字，而是处于等待连接的状态，实时监控网络状

态，等待客户端的连接请求。

2。客户端请求：指客户端的套接字提出连接请求，要连接的目标是服务器端的套接字。为此，客户端的套接字

必须首先描述它要连接的服务器的套接字，指出服务器端套接字的地址和端口号，然后就向服务器端套接字提

出连接请求。

3。连接确认：当服 务器端套接字监听到或者说接收到客户端套接字的连接请求时，就响应客户端套接字的请

求，建立一个新的线程，把服务器端套接字的描述发给客户端，一旦客户端 确认了此描述，双方就正式建立连

接。而服务器端套接字继续处于监听状态，继续接收其他客户端套接字的连接请求。


#4，http连接


HTTP协议是建立在TCP协议之上的一种应用，HTTP连接使用的是“请求—响应”的方式，不仅在请求时需要先建

立连接，而且需要客户端向服务器发出请求后，服务器端才能回复数据。在请求结束后，会主动释放连接。从

建立连接到关闭连接的过程称为“一次连接”。由于HTTP在每次请求结束后都会主动释放连接，因此HTTP连接

是一种“短连接”，要保持客户端程序的在线状态，需要不断地向服务器发起连接请求。通常的做法是即时不需

要获得任何数据，客户端也保持每隔一段固定的时间向服务器发送一次“保持连接”的请求，服务器在收到该请

求后对客户端进行回复，表明知道客户端“在线”。若服务器长时间无法收到客户端的请求，则认为客户端“下

线”，若客户端长时间无法收到服务器的回复，则认为网络已经断开。



#（5）TCP/IP协议和Http协议之间的关系：

TPC/IP协议是传输层协议，主要解决数据 如何在网络中传输，而HTTP是应用层协议，主要解决如何包装数

据，而socket则是对TCP/IP协议的封装和应用（程序员层面上）。实际上http协议就是建立在tcp/ip协议

之上的。关于TCP/IP和HTTP协议的关系：

“我们在传输数据时，可以只使用（传输层）TCP/IP协议，但是那样的话，如 果没有应用层，便无法识别数据

内容，如果想要使传输的数据有意义，则必须使用到应用层协议，应用层协议有很多，比如HTTP、FTP、

TELNET等，也 可以自己定义应用层协议。WEB使用HTTP协议作应用层协议，以封装HTTP文本信息，然后使用

TCP/IP做传输层协议将它发到网络上。”

#（6）Socket和TCP/IP协议之间的关系：

socket是对TCP/IP协议的封装，Socket本身并不是协议，而是一个调用接口（API），通过Socket，我们才

能使用TCP/IP协议。 实际上，Socket跟TCP/IP协议没有必然的联系。Socket编程接口在设计的时候，就希

望也能适应其他的网络协议。所以说，Socket的出现 只是使得程序员更方便地使用TCP/IP协议栈而已，是对

TCP/IP协议的抽象，从而形成了我们知道的一些最基本的函数接口，比如create、 listen、connect、

accept、send、read和write等等。网络有一段关于socket和TCP/IP协议关系的说法比较容易理 解：


“TCP/IP只是一个协议栈，就像操作系统的运行机制一样，必须要具体实现，同时还要提供对外的操作接口。

这个就像操作系统会提供标准的编程接口，比如win32编程接口一样，TCP/IP也要提供可供程序员做网络开发

所用的接口，这就是Socket编程接口。”

#（7）tcp/ip协议, http协议，socket三者之间的关系：

实际上，传输层的TCP是基于网络层的IP协议的，而应用层的HTTP协议又是基于传输层的TCP协议的，而

Socket本身不算是协议，它只是提供了一个针对TCP或者UDP编程的接口。

#（8）tcp协议和udp协议之间的区别：

TCP --- 传输控制协议,提供的是面向连接、可靠的字节流服务。当客户和服务器彼此交换数据前，必须先在

双方之间建立一个TCP连接，之后才能传输数据。TCP提供超时重发，丢弃重复数据，检验数据，流量控制等功

能，保证数据能从一端传到另一端。 理想状态下，TCP连接一旦建立，在通信双方中的任何一方主动关闭连接

前，TCP 连接都将被一直保持下去。断开连接时服务器和客户端均可以主动发起断开TCP连接的请求 

UDP --- 用户数据报协议，是一个无连接的简单的面向数据报的运输层协议。UDP不提供可靠性，它只是把应

用程序传给IP层的数据报发送出去，但是并不能保证它们能到达目的地。由于UDP在传输数据报前不用在客户

和服务器之间建立一个连接，且没有超时重发等机制，故而传输速度很快



TCP发送的包有序号，对方收到包后要给一个反馈，如果超过一定时间还没收到反馈就自动执行超时重发，因此

TCP最大的优点是可靠。一般网页（http）、邮件（SMTP)、远程连接(Telnet)、文件(FTP)传送就用TCP  

UDP是面向消息的协议，通信时不需要建立连接，数据的传输自然是不可靠的，UDP一般用于多点通信和实时的

数据业务，比如语音广播、视频、QQ、TFTP(简单文件传送）、SNMP（简单网络管理协议）、RTP（实时传送

协议）RIP（路由信息协议，如报告股票市场，航空信息）、DNS(域名解释）。注重速度流畅。 

#9,FTP协议：

文件传输协议（File Transfer Protocol, FTP）是TCP/IP网络上两台计算机传送文件的协议，FTP是在

TCP/IP网络和INTERNET上最早使用的协议之一，它属于网络协议组的应用层。FTP客户机可以给服务器发出

命令来下载文件，上载文件，创建或改变服务器上的目录。

参考  http://blog.csdn.net/lanhuzi9999/article/details/32713815

#说了一大包好像都没有在Android中具体运用到这些网络协议

#说说自定义协议吧

scoket的自定义协议可以通过 #包头+包体长度+包体


具体可以参考http://blog.csdn.net/lincyang/article/details/6109076
