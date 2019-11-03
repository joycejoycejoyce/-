# 网络编程
也算是一块考的超级频繁的内容。我常常在这一块被难住。也是时候一点点的看懂它了。

* 计算机网络：是指将地理位置不同的具有独立功能的多台计算机通过通信网络连接起来，在网络操作系统，
网络管理软件，以及网络通信协议的管理和协调下，实现资源共享和信息传递的计算机系统

* 网络编程
在网络networking protocols 下面，实现网络互连的不同计算机上运行的程序间可以进行数据交换
* 网络编程三要素
1. IP address. 
 在这样的一个网络中我们如何找到对方. (ComputerA & ComputerB). 
2. Port 
端口port 是对程序的唯一标识. 
网络的通信，本质上是两个应用程序的通信。每台计算机上都有很多的应用
程序。那么在网络通信时，如何区别这些应用程序呢？如果说IP address可以唯一标识网络中的设备，那么端口号port就可以唯一标识设备
中的application,是应用程序的标识.
### Intro 
端口号：  
   用两个字节表示的整数。它的取值范围是0～65535. 其中0-1023之间的端口号用于一些致命的网络服务和应用。
   如果端口号被另一个服务或者是应用所占用，会导致当前程序启动失败
3. protocol. 通信的规则


## TCP/IP 5 layers  
* user 
-------------------------------
1. application layer 

HTTP & HTTPS protocols 
- HTTP request 
- HTTPS encapsulation 
-------------------------------
2. transport layer

- TCP protocol
- three way handshake  
/*   why HTTP request is not placed in here? doesn't the request happens sequencially like this? */
- four way handshake 
- UDP protocol
packet = information in the envolop 

what packet contains: 
everything in the HTTP request 
-------------------------------
3. network layer 
IP 关心的是从A－> B的具体路径实现
"I want data flow from point A to point B" 

Topics: 
- IP protocol
* private IP address 
* public IP address 
* DNS 
-------------------------------
4. link layer 

Ethernet frame 
-------------------------------
5. physical layer 

electricity 
-------------------------------
hardware 

`
* 每一层都是完了完成一种功能。为了实现这些功能，就需要大家都遵守共同的规则。
互联网的每一层，都定义了很多协议。这些协议的总称，就叫做“互联网协议” （Internet Protocol Suite）. 他们是互联网的核心。

## Layer 1: Application Layer 
### HTTP vs HTTPS 协议protocol 
他们是 aset of conventions that web browsers and web servers use to speak to one another 

HTTP 报文是包裹在TCP报文中发送的。server 收到TCP报文是会解包提取出HTTP报文。
但是这个过程是有风险的。因为HTTP 报文是明文，如果中间被截取的话存在一定的信息泄露的风险。
所以在进入TCP报文之前做一次加密就可以解决这个问题了。HTTPS协议的本质就是HTTP＋SSL(or TLS). 
在HTTP报文进入TCP报文之前，先使用SSL对报文进行加密。它位于HTTP协议和TCP协议之间。

| HTTP          |
| ------------- |
| HTTP          | 
| TCP           |  
| IP            | 


| HTTPS         |
| ------------- |
| HTTP          | 
| SSL or TLS    |
| TCP           |  
| IP            | 


HTTPS 过程
HTTPS 在传输属区之前需要client 和server 进行一个 TLS／SSL握手。握手过程中将确立双方加密传输数据的密码信息。
TLS／SSL使用非对称加密，对称加密，和hash等。HTTPS 相对与HTTP尽管提供了安全保障，但是会带来一些时间上的损耗，比如说
握手和加密的过程。决定是否使用HTTPS其实是在安全和性能方面的权衡。 

### HTTP 简介
HTTP 协议 是 服务器传输Hyper Text 到本地Browser 的传送协议。
HTTP是基于TCP/IP通信协议来传递数据（HTML文件，img文件等等）.
client -- HTTP protocol ----> server 架构上
web server 有 Apache server, IIS server 等。
HTTP默认端口是80，但我可以自己改。

``` 
Web Browser <---> HTTP Server <----> CGI Program <-----> DB 

``` 

### HTTP 消息结构
是一个无状态的req/res protocol.
HTTP使用统一资源标识符URI 来传递数据和建立连接。
#### 客户端请求消息
client 发送一个HTTP请求到服务器的请求消息包括一下格式： request line + header + 空行＋请求数据
``` 
<request method> <URL> <protocol-version>  // request line 
<Header字段名>: <value>  // request header 
<Header字段名>: <value> // request header
// 空行
request data 
```

### 服务器相应消息
HTTP response 也由四部分组成： status row, 消息报头，空行，响应正文
```
HTTP/1.1 200 OK      // status row 

``` 



## Layer 2: Transport Layer 
* UDP 
* TCP "I want to make sure data get from point A to point B"
    TCP's purpose in life is to keep track of all the data that flows across the Internet between point A
    and point B, and if any packets get lost or corrupted or dropped by a firewall, if they disappear somewhere into the Ether. **The purpose of TCP is to tell computer A, "resend the same data to point B".** 


## Layer 3: Network Layer 
### Intro of IP address   
* IP address 相当于门牌号码，
通过IP address 才能知道每一个主机的位置。server 也是一个主机，想要访问某一个server, 必须直到server的IP address.

### Comparison between Private and Public IP Addresses 
* Private IP Address:
used to communicate within the same network 
* IP address 分为两大类
1. IPv4: 
给每个链接在网络上的主机分配了一个32bit的地址。按照TCP／IP的规定，IP地址用二进制来表示，每个IP地址长32bit,也就是4个bytes.
为了方便使用，IP地址经常被写成十进制的形式，中间用符号“.” 分隔不同的字节。
2. IPv6
现在对IP地址的需求量越来越大，但是网络资源地址有限，所以IP的分配变得越来越紧张。为了扩大地址空间，通过IPv6重新定义地址空间，采用128位地址长度，去解决网络地址资源数量不够的问题
虽然话是这么说，但其实基本上IPv6是不被使用的。因为router 并不明白IPv6.所以用IPv6常常会有问题。现在基本所有的通向网络的设备都还是用IPv4. 

* Public IP Address: 
used to communicate outside of the network 
Public IP address is basically assigned by the ISP (Internet Service Provider)
It's an address lots of people share 
search by type in "my ip address " in Chrome 

`
 ____                                   ____  
|    |                                 |    | 
|____|                                 |____|


  PC                                    Server 
California                            New York
private IP: 10.1.1.100                private IP: 192.168.1.121
public IP: 70.62.50.42                public IP: 40.20.26.63


`


| Public IP Address               | Private IP Address    | 
| -------------                   | ------------- | 
| Scope is global                 | Scope is local    |  
| It is used to communicate outside the network| It is used to communicate within the network|  
| Public IP may differ in uniform or non-uniform manner| Private IP addr of the systems connected in a network differ in a uniform mannaer|

|It is used to get internet service| It works only in LAN |
|search by google                 |Network Wifi Advance check |


### IP Protocols
* UDP protocol 
 UDP协议是User Datagram Protocol 
 它是无连接通信协议。即在数据传输时，数据的发送端和接收端不建立逻辑连接。
  简单的说，当PC A  －> PC B 时， 发送端不会确认接收端是否存在，就会发出数据。同样接收端在收到数据时，
  也不会向发送端反馈是否收到数据。
  由于UDP协议消耗资源小，通信效率高，所以通常会被用于audio, video 和普通data 的传输.
  比如视频会议通常采用UDP协议。因为即使丢失一两个数据包，也不会对接受结果产生太大的影响。但是使用UDP协议
  传送数据时，由于UDP的面向无连接性，不能保证数据的完整性。因此传输重要数据时不建议使用UDP协议。 
* TCP protocol 
  Transmission Control Protocol 
  TCP协议是面向连接的通信协议。在传输数据之前，在发送端和接收端必须要建立起逻辑联系。然后才能传输数据。
  它提供了两台计算机之间可靠无差错的数据传输。在TCP连接中必须要明确客户端和服务器端。由客户端向服务器端
  发出连接请求。每次连接的建立都需要经过三次握手

* 三次握手
   TCP协议中，在发送数据的准备阶段，客户端和服务器之间的三次交互。以保证连接的可靠。
  第一次握手：客户端向服务端发送连接请求，等待服务器确认
  第二次握手：服务器端想客户端送回一个响应，通知客户端收到了连接请求
  第三次握手：客户端再次向服务端发送确认信息，确认连接

  ` 
   1) client -- req: "request connect" --> server 
   2) client <--  res :"request received" -- server
   3) client -- conf"confirmation"  --> server 
  `

   三次握手完成后，连接就建立了。客户端和服务端就可以开始进行数据传输了。对于这种面向连接的特性，TCP协议可以
   保证传输数据的安全。所以应用十分广泛。例如上传文件，下载文件，浏览网页等等。

### 涉及的其他技术
* 127.0.0.1 IP Address 和 myIPAddress 区别

 127.0.0.1 is a special-purpose IPv4 address called localhost 
 All computers use this address as their own 
 Doesn't let them communicate with other devices as a real IP address does 
 only used by the computer u r on
 
 when is used?
 web server running on a computer can point to 127.0.0.1 so the page can be run locally and tested before it's deployed 

 application server -- message & IP address --> client 
 TCP/IP recognizes (127.0.0.1) as a special IP address 

 Messages sent to loopback IP addresses like 127.0.0.1 do not reach outside of the local area network 

 127.0.0.1 accessed through a loopback interface but not through the network adapter 
 this works even if there is no network chips in the system 

 system IP address 
  the ip you get from the router is a different story: it's the address that other computer on the network to find you 
  you can use this ip on the same machine too, but it works differently as before: it's going out to 
  the router and in again 



 * private IP address 
 private IP address: 192.168.1.115
 can communicate with a router and other networked devices 
localhost: 127.0.0.1 
attached to it to mean "this computer"

### TCP 通信程序
### TCP 通信原理
TCP通信协议是一种可靠的网络协议。它在通信的两端各建立一个Socket 对象，从而在通信的两端形成网络虚拟链路，
一旦建立了虚拟的网络链路，两端的程序就可以通过虚拟链路进行通信。 
Java 对基础TCP协议的网络提供了良好的封装，使用Socket 对象来表示两端的通信端口，并通过Socket 产生IO流来进行网络通信

A TCP connection consists of 4 parts:
1. Client IP 
2. Client Port 
3. Server IP 
4. Server Port 






## Layer 4: Link Layer 
## Layer 5: physical layer 
* 实体层就是把电脑连接起来的物理手段
* 它主要规定了网络的一些电气特性，作用是负责传送0&1的电信号
* 电脑要组成网络，第一件事就是要把电脑连起来。可以用光缆，电缆，双绞缆，无线电波等方式。


## Socket 
Socket 接口是TCP／IP 网络的API，Socket接口定义了许多函数或是例程，程序眼可以用他们来开发TCP/IP网络上的应用程序。
要学Internet 上的TCP／IP网络编程，必须理解Socket接口。



## 什么是URL
### Intro 
URL是Web的一个核心概念。它是Browser用来检索Web上公布的任何资源的机制。
URL指的是统一资源定位符（Uniform Resource Locator）. URL是一个给定的独特资源在Web上的地址。
这个资源可以是一个HTML页面，一个CSS文档，一个IMG，等等。

```
http://www.example.com:80/path/to/myfile.html?key1=value1&key2=value2#SomewhereInTheDocument
``` 
* protocol: 上面的`http://`是协议。
* domain name: `www.example.com`是域名 domain name。
* port: `:80` 是端口。它表示用于访问web 服务器上的资源的技术门。如果web服务器使用HTTP协议的标准端口 (
HTTP 为 80， HTTPS为443)来授予其资源的访问权限。
* `／path/to/myfile.html` 是网络服务器上的资源的路径。
* `？可以=value1&key2=value2`是提供给网络服务器的额外参数。这些参数是用`&` 分隔的key value pair. 
在返回资源之前，web server 可以使用这些参数执行额外的操作。每个web server都有自己关于参数的规则，唯一可靠的
方式来直到web server 是否处理参数是通过询问web server 的所有者。
* `#SomewhereInTheDocument`是资源本身另一部分的锚点。锚点表示资源中的一种书签。给浏览器显示位于该“加书签”位置的
内容的方向。例如在html文档上，browser 将滚动到定义锚点的位置。在视频或是音频文件傻姑娘，浏览器将尝试转到锚代表的
时间。指的注意的是， `#`后面的部分从来没有发送到server. 

 一个形象的方法想URL就是它类似于普通信件的地址。协议代表你要使用的邮政服务。域名是城市或是城镇。端口则像zip code.
 path 代表着我的信件所递送的大楼。参数提供额外的信息，比如大楼所在但远。最后，锚点表示信件的收件人。

## 域名是什么
### 解决的问题
对于互联网上连接的每一台电脑，我们都可以通过一个公共IP地址访问到。
IP address 由四组数字组成，中间用 dot 连接。计算机可以很容易的处理这些IP address。但是对于人类来说在使用过程中难记忆而且
容易输入错误。所以我们用alphabet & number 组合来代替纯数字的IP adress,比如我们只会记住www.google.com 而不会去记忆 888.20.434.123. 这个人类可读的地址，就称作域名。

### Intro 
` developer.mozilla.org` => structure : `label2.label1.TLD`
* TLD (aka Top-Level Domain, 顶级域名);  
TLD提供了最多的信息。TLD告诉用户通用服务背后的域名。最通用的顶级域名(.com, .org, .net). 不需要web server 满足
严格的标准。
* 标签 label1, label2   
label 都是跟着TLD的。一个标签可以是任何东西，从一个字母到一个句子。
### DNS 请求如何工作
过程就是
1. 在浏览器输入域名 `mozilla.org`;
2. 您的浏览器询问计算机是否识别此域名所确定的IP address （使用本地DNS缓存）. 如果是的话，这个域名被转换成IP address，然后进行到下一步的建立连接环节 (三次握手). 
3. 如果我的电脑不知道`mozilla.org`所对应的IP, 它会询问一个LDNS，然后LDNS找到了我们就进行到下一步的建立连接环节。
4. 如果没有我就回去找根服务器，然后根服务器去找顶级域名服务器。然后我会找到相应的com 域名的顶级服务器地址
5. 最后在相应的com 域名的顶级服务器中找到对应的IP address，传回我的电脑，我的电脑再传回给我的Browser




## 讲讲 get 和 post 的区别 
这里说的GET 和 POST 特指浏览器中的HTTP request 而不是 Ajax 的HTTP request. 即是HTTP protocol 中的GET／POST.
浏览器用GET请求来获取一个html页面／img/css/js 等资源。用POST 来提交一个`<form>` 表单,并得到一个结果的网页。
### DEF
GET的定义:
"read" 一个资源。比如GET到一个HTML 文件。因为GET是读取，所以可以对GET请求的数据做缓存。这个缓存可以做到Browser上（
彻底避免Browser 重复的request），也可以做到代理上（nginx），或者做到server 端。

POST的定义：
POSt是不能够被随意的执行多次的。所以不能缓存。比如说server 创建了新的订单，然后返回order success page. 这个页面不可以
被缓存。

### Comparison
* 安全性：  
我们常说GET 不如POST 安全。因为POST用body传输数据，而GET用url传输。更容易被看到。但是其实从攻击的角度来看，不论是GET或是POST都不是很安全。因为HTTP本身就是明文协议。
每个HTTP请求和返回的每个byte 在网络上都是明文传播。不论是url,header 或是body. 所以想要提高安全性，不如使用HTTPS协议来得更安全。



## 状态代码的意义

| status        | meaning           | 
| ------------- | ------------------|            
| 1XX           | 指定信息:标识请求已接受，继续处理    | 
| 2XX           | 成功：表示请求已经被成功接受，理解，接受     |   
| 3XX            | 重新定向：要完成请求必须进行更进一步的操作             | 
| 4XX            | 客户端错误：请求有语法错误或请求无法实现             | 
| 5XX            | 服务器错误：服务器未能实现合法的请求             | 





## 从输入URL到页面加载完成的过程中都发生了什么

### 相关的概念
3. DNS
每个Domain都对应一个或者是多个提供相同服务服务器的IP地址，只有知道了服务器的IP地址才能建立连接。所以需要通过DNS
 想要获得server 的ip address， 需要将 domain (https://google.com) -> IP address (888.20.434.123)

### 概述
1. DNS 解析
2. TCP 连接：Broswer 根据IP address 与 server 建立 socket 连接
3. 发送HTTP请求： Browser 请求 
4. server 处理求求并返回HTTP 报文: server 处理请求
5. Brower parse && render page
6. 连接结束： Broswer 和 server 断开连接


1. DNS 解析：Broswer 查找domain 相对的IP address 
DNS解析的过程就是寻找哪台机器上有你需要的资源的过程。
DNS: Domain  --> IP address 
查找过程
 1. Browser搜索自己的DNS缓存 (有一张 Domain 与 IP address 地址的对应表)。
 2. search OS 中的DNS 缓存。
 3. 搜索OS 的 hosts 文件。
 4. OS 将 domain 发到LDNS（本地区域名服务器，如果我在学校接入Internet，那么LDNS服务器就在学校）。 LDNS查询自己的
 DNS缓存，（这个查找的成功率在80%左右）。如果查找成功返回结果，是被就发起一个iterative DNS parse request. 
  1) LDNS 向 Root Name Server （根域名服务器，虽然没有每个Domain的具体信息，但是存储了负责每个Domain，比如说com, net, org 等的解析的顶级域名服务器的地址） 发起请求。这里，Root Name Server 返回 com 域名的顶级域名服务器的地址
  2） LDNS 向 com 域的顶级域名服务器发起请求，返回google.com 域名服务器地址
  3）LDNS向google.com 域名服务器发起请求，得到了www.google.com 的IP address
  5. LDNS把这个IP address 返回给OS，自己也把这个IP address 缓存起来
  6. OS 将 IP address 还给 browser， 然后自己也把 IP address 缓存起来
  7. 这样，浏览器就得到了域名相对应的IP 地址

``` 
Browser         
1. search DNS 缓存
        ＝> OS 
        2. search DNS 缓存
            ＝> hosts 
                3. 搜索 hosts 文件
                    ＝>  LDNS 本地区域名服务器
                         4. search DNS 缓存
                                ＝> Root Name Server 
                                    5. 帮助找到相应的顶级域名服务器
                                        => 顶级域名服务器
                                        knows everything end with the top-level domain 
                                            6. 找到网站域名服务器
                                                ＝> google.com 域名服务器

                                                                root DNS 
                                                                (final .)
                                                    7. find IP 
        OS<＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝ IP      
        8. return IP 
 <======                     
 browser
 9. return IP   
``` 
  补充说明：
  * 域名和URL是两个概念。域名是一台或是一组服务器的名称。用来确定server 在 Internet 上的位置。
    URL是统一资源定位符，用来确定某一个文件的具体位置。  
    eg: zhihu.com 是知乎的域名。根据这个域名可以找到知乎的服务器。
        zhihu.com/people/compileyouth 是一个URL，可以根据这个URL定位到某一个用户的知乎页面

  * IP address 和 domain name 不是一一对应的关系： 我们可以吧多个提供相同服务的server IP set as the same domain name. 但是同一时刻，一个domain name 只能parse one IP address. 同时，一个 IP address 可以绑定多个domain name, 数量不限制。




  建立连接
  知道了server 的 IP address，下面就开始和服务器建立连接了。 
  通俗的讲，通信连接的建立需要经历三个过程。
  1. client --- " Hello, I want to know u " ---> server 
  2. client <---" Nice to meet u  " --------- server 
  3.  client ---- " Nice to meet u too " ------> server 
  补充：
  * TCP 协议： 三次握手的过程采用TCP协议。其可以保证信息传输的可靠性。三次握手过程中，
  如果一方收不到确认信号，协议会要求重新发送信号。

3. 网页请求与显示
  连接建立后，就开始了client & server 的通信。webpage request 是一个单向请求的过程，即一个client 向 server request data, and server returns responding data 的过程。
  1. broswe 根据url 内容生成HTTP request, request 中包含请求文件的位置，请求文件的方式等等。
  HTTP请求报文是由三部分组成： 请求头，请求报文，和请求正文。

  2. server 接到了请求后，会根据HTTP请求中的内容来决定如何获取相应的html文件
  3. server 将得到的HTML文件发送给Browser
  4. 在Browser 还没有完全接收 html file 时开始render网页
  5. 在读取html ccode 中，根据需要browser 会继续请求img, css, js 等文件。

  断开连接-- 四次挥手
  1. client ---- " i need to go, it's getting late " --> server 
  2. client <-- "okie, gotcha"  -- server
  3. client  <-- "i need to leave as well" --- server 
  4. client 断开连接
            -- "confirmation: break " --> server 


PS: 
* 为什么client在收到断开请求后不立即同意断开。当client收到断开connection的request时，可能仍有数据没有发送完毕，
所以client要先发送确认信号。等所有数据发送完毕之后再同意断开。




## TCP/IP  
it is not a single networking protocol 
it is a suite of protocols named after the two most important protocols or layers within it -- TCP & IP
`
HTTP 
assum all bottom layers work fine
---------------------------------------------------------

 
---------------------------------------------------------
Ethernet   

`
* communication =   message+ 
                    means to transmit 

THe TCP layer handles the msg part 
IP layer handles the means of transmission part 
TCP/IP is considered a stateless protocol suite because each client connection is newly made without
regard to whether a previous connection had been established





1. application layer 
the topmost layer is the application layer.
规定了应用程序的数据格式，把数据格式放入UDP或是TCP协议的Data中。比如TCP协议可以为不同程序传递数据
eg: HTTP -> website，是浏览器和服务器约定的一种数据格式。 

SMTP -> email 

2. transport layer 
TCP, UDP 
TCP (transmission control protocol) breaks msgs into small packets of dta
then reassumbles those packets into the original msg
IP 
ensures each package gets to the correct destination  
3. Internet Layer 
IP 
packet knows where it came from and where it's going 
This is done by means of a unique IP address assigned to each and every active recipient on the network
4.
 
### 
1. LAN (aka Local Area Network) & WAN (aka Wide Area Network)

2. socket 
end point of communication 
to send and receive msg over a network, it will have a socket at both the ends that  is the 
sender end as well as the receiver end.

inputstream -> reading data 
outputstream -> writing / sending data 


 
## SSH 
It is a method for secure remote login from one computer to another 

### Typical uses of the SSH protocol
The protocol is used in corporate networks for: 
* providing secure access for users and automated processes 



## 强制缓存 vs 协商缓存
### intro to caching 