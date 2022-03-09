# 网页制作
HTML: 是一种用于创建网页的标准标记语言
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="gbk">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>标题</title>
</head>
<body>
    <h1>我的第一个标题</h1>
    <p>我的第一个段落</p>
</body>
</html>
```
<a href="http://ulweb.club:8080/1.html">上述程序演示</a>

# __The Internet__

打开浏览器，输入网站的网址，按下回车，就可以访问到网站。

输入网址之后，并按下回车键之后，在我们看来短暂的一瞬间，发生了这些事：
1. 向DNS服务器查询Web服务器的IP地址
2. 浏览器根据返回IP建立TCP连接
3. 浏览器发送HTTP请求消息
4. 服务器返回HTTP响应消息
5. 浏览器解析响应消息并显示网页
6. 收发结束，释放TCP连接

python模拟一段客户端（浏览器）的上述过程
```python
import socket

if __name__ == '__main__':
    # 1. 向DNS服务器查询Web服务器的IP地址
    ip = socket.gethostbyname('dan-k391.github.io')
    port = 8080

    # 2. 浏览器根据返回IP建立TCP连接
    clientSocket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    # socket.AF_INET 是指使用 IPv4 地址
    # socket.SOCK_STREAM 是指使用 TCP 连接 
    clientSocket.connect((ip, port))

    # 3. 浏览器发送HTTP请求消息
    clientSocket.send(....)

    # 4. 接收服务器返回的HTTP响应消息
    clientSocket.recv(....)

    # 浏览器解析响应消息并显示网页的过程就不写在这里面了
    
    # 5. 断开连接
    clientSocket.close()
```

python模拟一段服务端的上述过程
```python
import socket

if __name__ == '__main__':
    # 1. 向DNS服务器查询Web服务器的IP地址
    ip = socket.gethostbyname('dan-k391.github.io')
    port = 8080

    # 2. 创建套接字
    serverSocket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    # socket.AF_INET 是指使用 IPv4 地址
    # socket.SOCK_STREAM 是指使用 TCP 连接 
    serverSocket.bind(('0.0.0.0', port))

    # 3. 等待客户端的请求
    serverSocket.listen(10)

    # 4. 接受客户端的请求
    clientSocket, addr = serverSocket.accept() 
    
    # 5. 断开连接
    serverSocket.close()
```

## 向DNS服务器查询Web服务器的IP地址
- DNS: Domain Name System 域名系统

1. TCP/IP网络  
   TCP/IP的结构就是由一些小的子网，通过路由器连接起来组成一个大的网络
2. IP地址  
   IP地址就相当于现实中一条街上的“XX号XX室”  
   其中"号"对应的号码是分配给整个子网的，而"室"对应的号码是分配给子网中的计算机的
   “号”称为网络号，“室”称为主机号
   IP地址 = 网络号 + 主机号
3. IP地址的结构  
   IP地址主体的表示方法
   ```
   10.20.50.169
   ```
   IP地址主体 + 子网掩码
   ```
   10.20.50.169/255.255.248.0
   ```
   子网掩码也可以用比特位进行表示
   ```
   10.20.50.169/21
   ```
   主机号比特位全部为0时代表整个子网
   ```
   10.20.48.0
   ```
   主机号比特位全部为1时代表对整个子网进行广播
   ```
   10.20.63.255
   ```

4. 域名解析  
   通过socket库向DNS服务器发出查询  
   socket库就是用于调用网络功能的程序组件集合  
   通过DNS查询IP地址的过程叫做域名解析  

   以下是简单的python DNS解析器
   ```python
   import socket

   if __name__ == '__main__':
      ip = socket.gethostbyname('dan-k391.github.io')
      print(ip)
   ```
5. 获取DNS服务器的IP地址  
   ![假如说显示不出来就点下面的链接](http://ulweb.club:8080/DNS.png)  
   <a href="http://ulweb.club:8080/DNS.png">假如说显示不出来就点我</a>

## 浏览器根据返回IP建立TCP连接
- 著名的三次握手
1. 客户端向服务器发送一个SYN J
2. 服务器向客户端响应一个SYN K，并对SYN J进行确认ACK J+1
3. 客户端再向服务器发一个确认ACK K+1  
   ![假如说显示不出来就点下面的链接](http://ulweb.club:8080/TCP.png)  
   <a href="http://ulweb.club:8080/TCP.png">假如说显示不出来就点我</a>  


## 发送HTTP请求消息
- URL: Uniform Resource Locator 统一资源定位符 (其实就是网址)
- HTTP: Hypertext Transfer Protocol 超文本传输协议
- 协议：通信操作的规则定义称为协议（protocol）  

1. 浏览器对URL进行解析  
   https:// ***dan-k391.github.io*** */theinternet/* index.html  
   在这个URL中：
      - https 是协议
      - dan-k391.github.io 是web服务器名
      - /theinternet/ 是目录名
      - index.html 是文件名
2. 有时URL会省略文件名  
   https://dan-k391.github.io/theinternet/ 省略了访问文件名， 就会访问默认文件，也就是index.html或default.htm。  
   https://www.baidu.com 只有服务器名，没有路径时就会访问根目录下事先设置的默认文件，也就是index.html或default. htm。  
3. 关于http  
   HTTP请求消息包含『对什么』和『进行怎样的操作』两个部分。
   其中相当于『对什么』的部分称为URI。  
   一般来说URI的内容是一个存放网页的文件名或者是一个CGI程序的文件名，例如"/dir/file.html"、"/dir/program.cgi"等。  
   其中『进行怎样的操作』的部分称为方法。  
   方法表示需要让web服务器完成怎样的工作，其中典型的例子包括读取URI表示的数据、将客户端输入的数据传递给CGI程序等。
   - URI: Uniform Resource Identifier 统一资源标识符
   - CGI程序：对web服务器程序调用其他程序的规则所做的定义就是CGI，安装这个规则来工作的程序就是CGI程序。
   - CGI程序使网页具有交互功能。
4. 生成HTTP请求消息  
   HTTP的主要方法
      - GET 获取URI的指定信息
      - POST 从客户端向服务端发送数据

   以下是一个HTTP 请求消息
   ```http
   GET /hello.html HTTP/1.1
   User-Agent: curl/7.16.3 libcurl/7.16.3 OpenSSL/0.9.7l zlib/1.2.3
   Host: http://43.154.73.126:8080
   Accept-Language: en, mi
   ```

## 接受HTTP响应消息
HTTP 响应消息
```http
HTTP/1.1 200 OK
Date: Thu, 10 Mar 2022 18:45:56 GMT
Server: Apache
Last-Modified: Thu, 10 Mar 2021 18:45:56 GMT
ETag: "34aa387-d-1568eb00"
Accept-Ranges: bytes
Content-Length: 51
Vary: Accept-Encoding
Content-Type: text/plain

<html>
.....
</html>
```

## 浏览器解析响应消息并显示网页
## 收发结束，释放连接
这两步就不赘述了 (

# HTML基础
## 前置插件，方便写
- live server
- live sass compiler


## HTML基础元素
```html
<h1>这是一个标题</h1>
<h2>这是一个标题</h2>
<h3>这是一个标题</h3>
<p>这是一个段落。</p>
<p>这是另外一个段落。</p>
<a href="https://www.baidu.com">这是一个链接</a>
```
<a href="http://ulweb.club:8080/2.html">上述程序演示</a>

## HTML属性

属性|描述
class|为html元素定义一个或多个类名（classname）(类名从样式文件引入)  
id|定义元素的唯一id  
style|规定元素的行内样式(inline style)  
title|描述了元素的额外信息 (作为工具条使用)  
```html

```




