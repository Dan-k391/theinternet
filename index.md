# __The Internet__

打开浏览器，输入网站的网址，按下回车，就可以访问到网站。

输入网址之后，并按下回车键之后，在我们看来短暂的一瞬间，发生了这些事：
1. 生成HTTP请求消息
2. 

## 生成HTTP请求消息
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
3. 关于http  
HTTP请求消息包含『对什么』和『进行怎样的操作』两个部分。
其中相当于『对什么』的部分称为URI。  
一般来说URI的内容是一个存放网页的文件名或者是一个CGI程序的文件名，例如"/dir/file.html"、"/dir/program.cgi"等。  
其中『进行怎样的操作』的部分称为方法。  
方法表示需要让web服务器完成怎样的工作，其中典型的例子包括读取URI表示的数据、将客户端输入的数据传递给CGI程序等。
   - URI: Uniform Resource Identifier 统一资源标识符
   - CGI程序：对web服务器程序调用其他程序的规则所做的定义就是CGI，安装这个规则来工作的程序就是CGI程序。
   - CGI程序使网页具有交互功能。
1. 生成HTTP请求消息  
   以下是一个传递数据  
   HTTP 请求消息
   ```http
   GET /hello.html HTTP/1.1
   User-Agent: curl/7.16.3 libcurl/7.16.3 OpenSSL/0.9.7l zlib/1.2.3
   Host: http://139.224.67.191:8080
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


