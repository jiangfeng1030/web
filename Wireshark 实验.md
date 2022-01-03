# Wireshark 实验

## 数据链路层

### 实作一 熟悉 Ethernet 帧结构

使用 Wireshark 任意进行抓包，熟悉 Ethernet 帧的结构，如：目的 MAC、源 MAC、类型、字段等。

![image-20220102132353663](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220102132353663.png)

目的Mac：00:74:9c:9f:40:13

源Mac：e8:6a:64:50:ce:88

类型：0x0800

**你会发现 Wireshark 展现给我们的帧中没有校验字段，请了解一下原因。**

帧格式中是包含校验字段的，但是Wireshark在抓包的时候，自动将校验字段给过滤掉了。

### 实作二 了解子网内/外通信时的 MAC 地址

1.`ping` 你旁边的计算机（同一子网），同时用 Wireshark 抓这些包（可使用 icmp 关键字进行过滤以利于分析），记录一下发出帧的目的 MAC 地址以及返回帧的源 MAC 地址是多少？这个 MAC 地址是谁的？

![image-20220102134059972](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220102134059972.png)

![image-20220102135012647](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220102135012647.png)

我的ip是192.168.43.139  我ping的目的地址是192.168.43.40

从图中可以看到源mac地址是00:f4:8d:ed:a6:01 是我主机的mac地址  目的mac地址是a0:a4:c5:c6:94:6d 是旁边计算机的mac地址（处于同一子网）

2.然后 `ping qige.io` （或者本子网外的主机都可以），同时用 Wireshark 抓这些包（可 icmp 过滤），记录一下发出帧的目的 MAC 地址以及返回帧的源 MAC 地址是多少？这个 MAC 地址是谁的？

![image-20220102142354969](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220102142354969.png)

目的mac是32:ea:26:ba:2d:5e  这是棋歌的mac地址

源mac是00:f4:8d:ed:a6:01  这是我主机的地址

3.再次 `ping www.cqjtu.edu.cn` （或者本子网外的主机都可以），同时用 Wireshark 抓这些包（可 icmp 过滤），记录一下发出帧的目的 MAC 地址以及返回帧的源 MAC 地址又是多少？这个 MAC 地址又是谁的？

![image-20220102142821672](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220102142821672.png)

目的mac是32:ea:26:ba:2d:5e

源mac是00:f4:8d:ed:a6:01 是我主机的mac

​    **通过以上的实验，你会发现：**

1. **访问本子网的计算机时，目的 MAC 就是该主机的**
2. **访问非本子网的计算机时，目的 MAC 是网关的**

   **请问原因是什么？**

网关是一个子网的出入口，当访问非子网的计算机时，需要通过网关才能访问外网；而访问本子网时，则不需要经过网关到外网。

### 实作三 掌握 ARP 解析过程

1.为防止干扰，先使用 `arp -d *` 命令清空 arp 缓存

![image-20220102143409844](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220102143409844.png)

2.`ping` 你旁边的计算机（同一子网），同时用 Wireshark 抓这些包（可 arp 过滤），查看 ARP 请求的格式以及请求的内容，注意观察该请求的目的 MAC 地址是什么。再查看一下该请求的回应，注意观察该回应的源 MAC 和目的 MAC 地址是什么。

![image-20220102143632757](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220102143632757.png)

![image-20220102144759013](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220102144759013.png)

回应的源mac是a0:a4:c5:c6:94:6d   我ping的主机的地址

目的mac是00:f4:8d:ed:a6:01 是我主机的mac地址

3.再次使用 `arp -d *` 命令清空 arp 缓存

![image-20220102145003468](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220102145003468.png)

4.然后 `ping qige.io` （或者本子网外的主机都可以），同时用 Wireshark 抓这些包（可 arp 过滤）。查看这次 ARP 请求的是什么，注意观察该请求是谁在回应。

![image-20220102145254439](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220102145254439.png)

![image-20220102145240762](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220102145240762.png)

​    **通过以上的实验，你应该会发现，**

1. **ARP 请求都是使用广播方式发送的**
2. **如果访问的是本子网的 IP，那么 ARP 解析将直接得到该 IP 对应的 MAC；如果访问的非本子网的 IP， 那么 ARP 解析将得到网关的 MAC。**

​    **请问为什么？**

ARP解析是先看arp表中是否有目的地址，如果有就不需要再次建立联系了，可以获取到目的MAC。如果没有就需要发送ARP请求，来获取目的MAC。如果目的地址是属于同一个子网，则不行要通过网关就能够进行通信，而不在同一个子网中就需要通过网关才能够建立联系。

## 网络层

### 实作一 熟悉 IP 包结构

使用 Wireshark 任意进行抓包（可用 ip 过滤），熟悉 IP 包的结构，如：版本、头部长度、总长度、TTL、协议类型等字段。

![image-20220102153147141](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220102153147141.png)

**为提高效率，我们应该让 IP 的头部尽可能的精简。但在如此珍贵的 IP 头部你会发现既有头部长度字段，也有总长度字段。请问为什么？**

头部有一行是可选的，可以选择要或是不要。总长度展示了网络层所传输的数据。如果没有该部分，数据链路层在传输时会对数据进行填充，目的网络层不会把填充的部分给去掉。

### 实作二 IP 包的分段与重组

根据规定，一个 IP 包最大可以有 64K 字节。但由于 Ethernet 帧的限制，当 IP 包的数据超过 1500 字节时就会被发送方的数据链路层分段，然后在接收方的网络层重组。

缺省的，`ping` 命令只会向对方发送 32 个字节的数据。我们可以使用 `ping 202.202.240.16 -l 2000` 命令指定要发送的数据长度。此时使用 Wireshark 抓包（用 `ip.addr == 202.202.240.16` 进行过滤），了解 IP 包如何进行分段，如：分段标志、偏移量以及每个包的大小等

![image-20220102154509095](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220102154509095.png)

分段标志：0x00 前两个是保留位

偏移量是用来标识数据包在数据流中的位置，图片中偏移量为1480，表明该包位于数据流的1480号位置。每个包的大小是用Total Length来表示，它包含IP包头部及数据两个部分。

**分段与重组是一个耗费资源的操作，特别是当分段由传送路径上的节点即路由器来完成的时候，所以 IPv6 已经不允许分段了。那么 IPv6 中，如果路由器遇到了一个大数据包该怎么办？**

转发或者丢弃

### 实作三 考察 TTL 事件

在 IP 包头中有一个 TTL 字段用来限定该包可以在 Internet上传输多少跳（hops），一般该值设置为 64、128等。

在验证性实验部分我们使用了 `tracert` 命令进行路由追踪。其原理是主动设置 IP 包的 TTL 值，从 1 开始逐渐增加，直至到达最终目的主机。

请使用 `tracert www.baidu.com` 命令进行追踪，此时使用 Wireshark 抓包（用 `icmp` 过滤），分析每个发送包的 TTL 是如何进行改变的，从而理解路由追踪原理。 

![image-20220102155509313](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220102155509313.png)

![image-20220102155536311](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220102155536311.png)

![image-20220102155547893](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220102155547893.png)

![image-20220102155600204](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220102155600204.png)

可以看到，每经过一个路由，TTL会增加1，直到到达目的地址。

**在 IPv4 中，TTL 虽然定义为生命期即 Time To Live，但现实中我们都以跳数/节点数进行设置。如果你收到一个包，其 TTL 的值为 50，那么可以推断这个包从源点到你之间有多少跳？**

TTL的设置为每一跳-1，当TTL=50时，64-50=14，说明经过了14跳

## 传输层

### 实作一 熟悉 TCP 和 UDP 段结构

1.用 Wireshark 任意抓包（可用 tcp 过滤），熟悉 TCP 段的结构，如：源端口、目的端口、序列号、确认号、各种标志位等字段。

![image-20220102155936760](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220102155936760.png)

源端口：443
 目的端口：64762
 序列号：4215
 确认号：10206
 标志字段：URG（紧急位）、SYN（同步位）、ACK（确认位）、FIN（结束位）、RST（重置位）
 Windows:391

2.用 Wireshark 任意抓包（可用 udp 过滤），熟悉 UDP 段的结构，如：源端口、目的端口、长度等。

![image-20220102160837355](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220102160837355.png)

源端口：52464
 目的端口：53
 长度：39

### 实作二 分析 TCP 建立和释放连接

1.打开浏览器访问 qige.io 网站，用 Wireshark 抓包（可用 tcp 过滤后再使用加上 `Follow TCP Stream`），不要立即停止 Wireshark 捕获，待页面显示完毕后再多等一段时间使得能够捕获释放连接的包。

![image-20220102161616105](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220102161616105.png)

2.请在你捕获的包中找到三次握手建立连接的包，并说明为何它们是用于建立连接的，有什么特征。

![image-20220102161826277](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220102161826277.png)

第三次握手，同步位（SYN）是0，确认位（ACK）是1

3.请在你捕获的包中找到四次挥手释放连接的包，并说明为何它们是用于释放连接的，有什么特征。

![image-20220102162112516](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220102162112516.png)

TCP释放时，终止控制位FIN和ACK控制位为1

**去掉 `Follow TCP Stream`，即不跟踪一个 TCP 流，你可能会看到访问 `qige.io` 时我们建立的连接有多个。请思考为什么会有多个连接？作用是什么？**

访问网页是有多个连接组成的。每个连接传送完数据后就会断开。断开连接，由于页面已经被缓存下来，页面仍然存在。若要重新进行发送数据，就要再次进行连接。

这样的连接，是为了实现多个用户进行访问，对业务频率不高的场合，节省通道的使用。

**我们上面提到了释放连接需要四次挥手，有时你可能会抓到只有三次挥手。原因是什么？**

中间的两次握手合并成了一次握手。

客户端向服务端发送断开连接的请求为第一次挥手，服务端向客户端回复同意断开为第二次，然后服务端向客户端发送断开的请求为第三次挥手，客户端向服务端回复同意断开连接为第四次挥手。三次挥手是将服务器向客户端发送断开连接和回复同意断开连接合成一次挥手，其他两次挥手不变

## 应用层

应用层的协议非常的多，我们只对 DNS 和 HTTP 进行相关的分析。

### 实作一 了解 DNS 解析

1.先使用 `ipconfig /flushdns` 命令清除缓存，再使用 `nslookup qige.io` 命令进行解析，同时用 Wireshark 任意抓包（可用 dns 过滤）。

![image-20220102162518644](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220102162518644.png)

![image-20220102162637183](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220102162637183.png)

2.你应该可以看到当前计算机使用 UDP，向默认的 DNS 服务器的 53 号端口发出了查询请求，而 DNS 服务器的 53 号端口返回了结果。

![image-20220102162859994](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220102162859994.png)

3.可了解一下 DNS 查询和应答的相关字段的含义

6位的标志位
QR：查询/应答标志。0表示这是一个查询报文，1表示这是一个应答报文

opcode，定义查询和应答的类型。0表示标准查询，1表示反向查询（由IP地址获得主机域名），2表示请求服务器状态

AA，授权应答标志，仅由应答报文使用。1表示域名服务器是授权服务器

TC，截断标志，仅当DNS报文使用UDP服务时使用。因为UDP数据报有长度限制，所以过长的DNS报文将被截断。1表示DNS报文超过512字节，并被截断

RD，递归查询标志。1表示执行递归查询，即如果目标DNS服务器无法解析某个主机名，则它将向其他DNS服务器继续查询，如此递归，直到获得结果并把该结果返回给客户端。0表示执行迭代查询，即如果目标DNS服务器无法解析某个主机名，则它将自己知道的其他DNS服务器的IP地址返回给客户端，以供客户端参考

RA，允许递归标志。仅由应答报文使用，1表示DNS服务器支持递归查询

zero，这3位未用，必须设置为0
rcode，4位返回码，表示应答的状态。常用值有0（无错误）和3（域名不存在）

应答字段
域名，类型，生命周期，数据长度，地址
**你可能会发现对同一个站点，我们发出的 DNS 解析请求不止一个，思考一下是什么原因？**

这与DNS的解析过程有关。
1.DNS解析过程是先从浏览器的DNS缓存中检查是否有这个网址的映射关系，如果有，就返回IP，完成域名解析；
2.如果没有，操作系统会先检查自己本地的hosts文件是否有这个网址的映射关系，如果有，就返回IP，完成域名解析；
3.如果还没有，电脑就要向本地DNS服务器发起请求查询域名；本地DNS服务器拿到请求后，先检查一下自己的缓存中有没有这个地址，有的话直接返回；
4.没有的话本地DNS服务器会从配置文件中读取13个根DNS服务器的地址，然后向其中一台发起请求；直到获得对应的IP为止。

所以DNS解析的请求不止一个

### 实作二 了解 HTTP 的请求和应答

1.打开浏览器访问 qige.io 网站，用 Wireshark 抓包（可用http 过滤再加上 `Follow TCP Stream`），不要立即停止 Wireshark 捕获，待页面显示完毕后再多等一段时间以将释放连接的包捕获。

![image-20220102163218341](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220102163218341.png)

2.请在你捕获的包中找到 HTTP 请求包，查看请求使用的什么命令，如：`GET, POST`。并仔细了解请求的头部有哪些字段及其意义。

![image-20220102163401252](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220102163401252.png)

Accept:告诉WEB服务器自己接受什么介质类型

Content-Type:WEB 服务器告诉浏览器自己响应的对象的类型

Content-Length:WEB 服务器告诉浏览器自己响应的对象的长度

Cache-Control:用来指示缓存系统（服务器上的，或者浏览器上的）应该怎样
处理缓存

Host:客户端指定自己想访问的WEB服务器的域名/IP 地址和端口号

POST:请求的方式，其中包括URI和版本

3.请在你捕获的包中找到 HTTP 应答包，查看应答的代码是什么，如：`200, 304, 404` 等。并仔细了解应答的头部有哪些字段及其意义。

![image-20220102164128611](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220102164128611.png)

该应答包的应答代码为200，表示OK
头部字段的意义：
Server：服务器通过这个头告诉浏览器服务器的类型
Transfer-Encoding：告诉浏览器数据的传送格式
Date：当前的GMT时间
Content- Type：表示后面的文档属于什么MIME类型
Cache-Control：指定请求和响应遵循的缓存机制

**刷新一次 qige.io 网站的页面同时进行抓包，你会发现不少的 `304` 代码的应答，这是所请求的对象没有更改的意思，让浏览器使用本地缓存的内容即可。那么服务器为什么会回答 `304` 应答而不是常见的 `200` 应答？**

采用200应答就是要完全的将内容发送给客服端，而浏览器可以用cache对网页的数据进行缓存，不必每一项都向服务器进行请求。