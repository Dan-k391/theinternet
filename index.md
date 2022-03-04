# __The Internet__

打开浏览器，输入网站的网址，就可以访问到网站。这其中不到一秒的时间，发生了一系列操作。  

输入网址之后，发生了这些事：
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
https://dan-k391.github.io/theinternet/ 省略了访问文件名， 就会访问默认文件，也就是index.html或default.htm  
https://www.baidu.com 只有服务器名，没有路径时就会访问根目录下事先设置的默认文件，也就是index.html或default.htm  


