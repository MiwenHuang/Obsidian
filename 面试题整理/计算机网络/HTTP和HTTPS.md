# HTTP特性和简述
web上的通信都是建立在HTTP协议上的
1. 客户端发起HTTP协议
2. 服务器作出响应处理后，返回HTTP响应报文

特点
![[Pasted image 20231108171934.png]]
# HTTP/HTTPS的区别
![[Pasted image 20231108172045.png]]
# HTTPS
![[Pasted image 20231108172221.png]]
![[Pasted image 20231108172245.png]]
![[Pasted image 20231108172258.png]]


![[Pasted image 20231108173415.png]]

5. HTTP请求过程
首先，在浏览器输入URL之后，浏览器依次在浏览器缓存、系统缓存和路由器缓存中查找匹配的URL，若有，则直接在屏幕中显示出页面内容，如果没有则浏览器对域名进行解析，获取对应的IP地址

获得IP第之后，浏览器向服务器发起TCP连接，与浏览器建立TCP三次握手。握手成功后，浏览器向服务器发送HTTP请求，来请求服务端的数据包，服务器处理浏览器端的请求，将数据返回给浏览器

浏览器收到HTTP响应，查询状态，状态成功再读取页面内容、进行浏览器渲染，解析HTML源码等。不成功则弹出响应指示。最后关闭TCP连接

6. HTTP请求方法
![[Pasted image 20231108174352.png]]

7. HTTP keep-alive
8. cookie和session
![[Pasted image 20231108175240.png]]

