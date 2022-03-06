# __The Internet__

打开浏览器，输入网站的网址，按下回车，就可以访问到网站。

输入网址之后，并按下回车键之后，在我们看来短暂的一瞬间，发生了这些事：
1. 生成HTTP请求消息
2. 向DNS服务器查询Web服务器的ip地址
3. 

## 生成HTTP请求消息
- URL Uniform Resource Locator 统一资源定位符 (其实就是网址)
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
https://www.baidu.com 只有服务器名，没有路径时就会访问根目录下事先设置的默认文件，也就是index.html或default.htm。  
1. 关于http  
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

   以下是一个传递数据  
   HTTP 请求消息
   ```http
   GET /hello.html HTTP/1.1
   User-Agent: curl/7.16.3 libcurl/7.16.3 OpenSSL/0.9.7l zlib/1.2.3
   Host: http://43.154.73.126
   Accept-Language: en, mi
   ```
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
   ```

## 向DNS服务器查询Web服务器的IP地址
1. TCP/IP 网络  
   TCP/IP的结构就是由一些小的子网，通过路由器连接起来组成一个大的网络
2. IP地址  
   IP地址就相当于现实中一条街上的“XX号XX室”  
   其中"号"对应的号码是分配给整个子网的，而"室"对应的号码是分配给子网中的计算机的
3. IP地址的结构  
   ```
   10.20.
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
5. 获取DNS的IP地址  
   ![win10 DNS配置](http://43.154.73.126/DNS.png)


