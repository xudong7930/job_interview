
#1.什么是CSRF攻击？XSS攻击？如何防范？
```
CSRF:https://baike.baidu.com/item/CSRF/2735433
防范方式: CSRF TOKEN, 即提交表单时同时提交一段由服务端渲染表单时生成的token,通过校验token来防范csrf攻击

XSS:https://baike.baidu.com/item/xss/917356
简单来说,XSS就是正常页面执行了用户或黑客提交的前端代码,比如你用了eval('这里执行了用户提交的代码'),
或者你的页面正常解析了用户提交的html代码,如用户提交的个人信息是:<img src="广告连接"><script>window.href="恶意网站连接"</script>,
而你不加过滤转义就入库,然后页面正常解析html代码,最终用户访问这个页面就会跳转到恶意网站 ,这就是XSS
防范方式: 过滤&&转义用户输入(如htmlentities、htmlspecialchars),永久不要信任客户端
```

#2.http与https的主要区别
```
一、https协议需要到ca申请证书，一般免费证书很少，需要交费。
二、http是超文本传输协议，信息是明文传输，https 则是具有安全性的ssl加密传输协议。
三、http和https使用的是完全不同的连接方式，用的端口也不一样，前者是80，后者是443。
四、http的连接很简单，是无状态的；HTTPS协议是由SSL+HTTP协议构建的可进行加密传输、身份认证的网络协议，比http协议安全。

```

#3.对称加密和非对称加密的区别
```

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
502 网关超时
503 服务不可用
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
```

```

#7.PHP中发起http请求有哪几种方式？它们有何区别？
```
curl
stream流的方式
socket方式
```

#8.从用户在浏览器中输入网址并回车，到看到完整的页面，中间都经历了哪些过程。
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












