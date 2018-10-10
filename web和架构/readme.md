
#1.什么是CSRF攻击？XSS攻击？Xpath攻击? 如何防范？
```
CSRF:https://baike.baidu.com/item/CSRF/2735433
防范方式: CSRF TOKEN, 即提交表单时同时提交一段由服务端渲染表单时生成的token,通过校验token来防范csrf攻击

XSS:https://baike.baidu.com/item/xss/917356
简单来说,XSS就是正常页面执行了用户或黑客提交的前端代码,比如你用了eval('这里执行了用户提交的代码'),
或者你的页面正常解析了用户提交的html代码,如用户提交的个人信息是:<img src="广告连接"><script>window.href="恶意网站连接"</script>,
而你不加过滤转义就入库,然后页面正常解析html代码,最终用户访问这个页面就会跳转到恶意网站 ,这就是XSS
防范方式: 过滤&&转义用户输入(如htmlentities、htmlspecialchars),永久不要信任客户端

Xpath攻击: https://blog.csdn.net/quiet_girl/article/details/50588130
```

#2.http与https的主要区别
* https://www.itcodemonkey.com/article/4195.html

```
一、https协议需要到ca申请证书，一般免费证书很少，需要交费
二、http是超文本传输协议，信息是明文传输，https 则是具有安全性的ssl加密传输协议
三、http和https使用的是完全不同的连接方式，用的端口也不一样，前者是80，后者是443
四、http的连接很简单，是无状态的；HTTPS协议是由SSL+HTTP协议构建的可进行加密传输、身份认证的网络协议，比http协议安全

```

#3.对称加密和非对称加密的区别
```
对称加密的意思就是，加密数据用的密钥，跟解密数据用的密钥是一样的

非对称加密的意思就是，加密数据用的密钥（公钥），跟解密数据用的密钥（私钥）是不一样的
```

#4.http状态码及其含意
```
200 请求已成功

301 永久重定向
302 临时重定向 
303 临时重定向，要求用get请求资源
304 not modified, 返回缓存，和重定向无关
307 临时重定向,严格不从post到get

400 参数错误
401 未通过http认证
403 未授权
404 不存在资源
500 内部错误
502 网关错误
503 无法处理当前请求
504 网关超时
```

#5.http协议的header中有哪些key及含义
```
# general
Request URL: http://app.io/
Request Method: GET
Status Code: 200 OK
Remote Address: 192.168.10.10:80
Referrer Policy: no-referrer-when-downgrade

# response header
Cache-Control: no-cache, private
Content-Type: application/json
Date: Wed, 26 Sep 2018 04:41:43 GMT
Server: nginx/1.13.6

# request header
Provisional headers are shown
DNT: 1
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Safari/537.36
```


#6.在HTTP通讯过程中，是客户端还是服务端主动断开连接？

* OSI七层协议模型、TCP/IP四层模型学习笔记 https://blog.csdn.net/guoguo527/article/details/52078962

* TCP的三次握手(建立连接）和四次挥手(关闭连接） https://www.cnblogs.com/Jessy/p/3535612.html

```
三次握手 客户端：我要和你通信(syn-sent) 服务端：你的请求已收到，发送确认(syn-rcvd) 客户端：你的确认已收到，连接建立(est)

四次挥手 客户端：我没有东西了，准备关闭(fin-wait) 服务端：你的关闭我收到了，但我还有点东西没传完(close-wait) ……一段时间后…… 服务端：我的东西传完了，可以关闭了(last-ack) 客户端：收到关闭通知，你也可以关闭了(time-wait)
```

#7.PHP中发起http请求有哪几种方式？它们有何区别？
```
curl
stream流的方式
socket方式
```

#8.从用户在浏览器中输入网址并回车，到看到完整的页面，中间都经历了哪些过程
```
浏览器->url->dns->ip->port->tcp->nginx->server name->php-fpm/fast cgi->php
   ^  <-  client ip:port        
```

#9.https 的加密过程？
```

```

#10.HTTP Method
```
get: 获取资源，不携带http body,支持查询参数，大小2KB
post: 传输资源，http body, 大小默认8M，1000个input variable
put: 传输资源，http body，资源更新
delete: 删除资源,不携带http body
patch: 传输资源，http body，存在的资源局部更新
head: 获取http header,不携带http body
options: 获取支持的method,不携带http body
trace: 追踪，返回请求回环信息,不携带http body
connect: 建立隧道通信
```

#11.cookie和session
```
cookie数据存放在客户的浏览器上，session数据放在服务器上
cookie不是很安全，别人可以分析存放在本地的COOKIE并进行COOKIE欺骗，考虑到安全应当使用session
session会在一定时间内保存在服务器上当访问增多，会比较占用你服务器的性能，考虑到减轻服务器性能方面，应当使用COOKIE
单个cookie保存的数据不能超过4K，很多浏览器都限制一个站点最多保存20个cookie

PHP为session的存储提供了三种方式: 文件/ 内存/ 自定义存储

#session
session_start();
$_SESSION['data']=1;
unset($_SESSION['data']);
session_destroy();

#cookie
setcookie('username', 'sbjsw', time()+3600, '/', 'vultr.com');
setcookie('username', '', time()-100);
$_COOKIE["username"];
```

#12.get和post
```
get是从服务器上获取数据，post是向服务器传送数据
get是把参数数据队列加到提交表单的ACTION属性所指的URL中，值和表单内各个字段一一对应，在URL中可以看到post是通过HTTP post机制，将表单内各个字段与其内容放置在HTML HEADER内一起传送到ACTION属性所指的URL地址用户看不到这个过程
get传送的数据量较小，不能大于2KBpost传送的数据量较大，一般被默认为不受限制4.. get安全性非常低，post安全性较高但是执行效率却比Post方法好
```

#13.如何处理负载、高并发?
```
HTML静态化 其实大家都知道，效率最高、消耗最小的就是纯静态化的html页面，所以我们尽可能使我们的 网站上的页面采用静态页面来实现，这个最简单的方法其实也是最有效的方法。

图片服务器分离 把图片单独存储，尽量减少图片等大流量的开销，可以放在一些相关的平台上，如骑牛等

数据库集群和库表散列及缓存 数据库的并发连接为100，一台数据库远远不够，可以从读写分离、主从复制，数据库集群方面来着手。另外尽量减少数据库的访问，可以使用缓存数据库如memcache、redis。

镜像： 尽量减少下载，可以把不同的请求分发到多个镜像端。

负载均衡： Apache的最大并发连接为1500，只能增加服务器，可以从硬件上着手，如F5服务器。当然硬件的成本比较高，我们往往从软件方面着手。 负载均衡建立在现有网络结构之上，它提供了一种廉价有效透明的方法扩展网络设备和服务器的带宽、增加吞吐量、加强网络数据处理能力，同时能够提高网络的灵活性和可用性。目前使用最为广泛的负载均衡软件是Nginx、LVS、HAProxy。
```

#14.代理
* https://www.cnblogs.com/Anker/p/6056540.html


#15.系统架构设计中缓存的使用方式
* https://zhuanlan.zhihu.com/p/40091810
```
为什么使用缓存?
提升性能：使用缓存可以跳过数据库查询，分布式系统中可以跳过多次网络开销。在读多写少的场景下，可以有效的提高性能，降低数据库等系统的压力。

缓存的适用场景?
1.数据不需要强一致性
2.读多写少，并且读取得数据重复性较高
```

#16.Websocket、Long-Polling、Server-Sent Events(SSE) 区别
```
普通的http：
    1.客户端从服务器端请求网页
    2.服务器作出相应的反应
    3.服务器返回相应到客户端

AJAX 轮询:
    1.客户端使用普通的http方式向服务器端请求网页
    2.客户端执行网页中的JavaScript轮询脚本，定期循环的向服务器发送请求（例如每5秒发送一次请求），获取信息
    3.服务器对每次请求作出响应，并返回相应信息，就像正常的http请求一样

AJAX 长轮询:
    1.客户端使用普通的http方式向服务器端请求网页
    2.客户端执行网页中的JavaScript脚本，向服务器发送数据、请求信息
    3.服务器并不是立即就对客户端的请求作出响应，而是等待有效的更新
    4.当信息是有效的更新时，服务器才会把数据推送给客户端
    5.当客户端接收到服务器的通知时，立即会发送一个新的请求，进入到下一次的轮询

Server Sent Events (SSE): 
    1.客户端使用普通的http方式向服务器端请求网页
    2.客户端执行网页中的JavaScript脚本，与服务器之间建立了一个连接
    3.当服务器端有有效的更新时，会发送一个事件到客户端

HTML5 Websockets:
    1.客户端使用普通的http方式向服务器端请求网页
    2.客户端执行网页中的JavaScript脚本，与服务器之间建立了一个连接
    3.服务器和客户端之间，可以双向的发送有效数据到对方

WebRTC:
    WebRTC是一种点对点类型的传输方式，它支持多种传输协议，如：UDP、TCP甚至是抽象层的协议。设计它时同时考虑到了允许使用可靠和不可靠的两种方式传输数据。这种技术一般应用在传输数据量较大的内容，比如音、视频等流媒体的传输

Comet:
Comet是一种用于web的推送技术，能使服务器实时地将更新的信息传送到客户端，而无须客户端发出请求，目前有两种实现方式，长轮询和iframe流
    1.iframe流方式是在页面中插入一个隐藏的iframe，利用其src属性在服务器和客户端之间创建一条长链接，服务器向iframe传输数据（通常是HTML，内有负责插入信息的javascript），来实时更新页面
    2.长轮询是在打开一条连接以后保持，等待服务器推送来数据再关闭的方式。
```

#17.nginx和lvs负载均衡比较?
```
LVS的特点是：
    1、抗负载能力强、是工作在网络4层之上仅作分发之用，没有流量的产生；
    2、配置性比较低，这是一个缺点也是一个优点，因为没有可太多配置的东西，
       所以并不需要太多接触，大大减少了人为出错的几率；
    3、工作稳定，自身有完整的双机热备方案；
    4、无流量，保证了均衡器IO的性能不会收到大流量的影响；
    5、应用范围比较广，可以对所有应用做负载均衡；
    6、LVS需要向IDC多申请一个IP来做Visual IP，因此需要一定的网络知识，所以对操作人的要求比较高。

Nginx的特点是：
    1、工作在网络的7层之上，可以针对http应用做一些分流的策略，比如针对域名、目录结构；
    2、Nginx对网络的依赖比较小；
    3、Nginx安装和配置比较简单，测试起来比较方便；
    4、也可以承担高的负载压力且稳定，一般能支撑超过1万次的并发；
    5、Nginx可以通过端口检测到服务器内部的故障，
       比如根据服务器处理网页返回的状态码、超时等等，
       并且会把返回错误的请求重新提交到另一个节点，不过其中缺点就是不支持url来检测；
    6、Nginx对请求的异步处理可以帮助节点服务器减轻负载；
    7、Nginx能支持http和Email，这样就在适用范围上面小很多；
    8、不支持Session的保持、对Big request header的支持不是很好，
    另外默认的只有Round-robin和IP-hash两种负载均衡算法。
```


#18.javascript跨域？
```
jsonp, cors
```

#19.出现性能瓶颈如何快速定位解决？
```
服务器负载 慢日志 xhprof 慢sql
xhprof性能分析: https://blog.csdn.net/qq_28602957/article/details/72697901
```

#20.微服务
```
https://blog.csdn.net/wuxiaobingandbob/article/details/78642020?locationNum=1&fps=1
```