---
layout: post
title:  "DNS协议"
date:   2018-06-10 11:05:00 +0800
categories: blog
---
DNS协议
========================================  


简介：
---------
DNS是域名系统(DomainNameSystem)的缩写，该系统用于命名组织到域层次结构中的计算机和网络服务。

域名是由圆点分开一串单词或缩写组成的，每一个域名都对应一个惟一的IP地址，在Internet上域名与IP地址之间是一一对应的，DNS就是进行域名解析的服务器。

DNS命名用于Internet等TCP/IP网络中，通过用户友好的名称查找计算机和服务。

DNS是因特网的一项核心服务,它作为可以将域名和IP地址相互映射的一个分布式数据库。

细节
--------
**1.DNS使用的协议**


DNS在进行区域传输的时候使用TCP协议，其它时候则使用UDP协议；

DNS主要还是使用UDP，解析器还是服务端都必须自己处理重传和超时。DNS往往需要跨越广域网或互联网，分组丢失率和往返时间的不确定性要更大些，这对于DNS客户端来说是个考验，好的重传和超时检测就显得更重要了。

DNS协议的相关RFC文档：
 
　RFC1034-《DOMAIN NAMES - CONCEPTS AND FACILITIES》
 
　RFC1035-《DOMAIN NAMES - IMPLEMENTATION AND SPECIFICATION》 


**2.域名**

现代因特网采用层次树状结构的命名方法，任何一个连接在因特网上的主机或路由器，都有一个唯一的层次结构的名字，该名字称为域名。

![icon](https://img-blog.csdn.net/20140517195630812)



+ 域名的分级
 ----------
域名可以划分为各个子域，子域还可以继续划分为子域的子域，这样就形成了顶级域、二级域、三级域等。
![icon2](https://img-blog.csdn.net/20140517200841796)
 其中顶级域名分为：国家顶级域名、通用顶级域名、反向域名。

 国家顶级域名：中国:cn， 美国:us，英国uk...

 通用顶级域名：com 公司企业  edu教育机构 gov政府部门  int国际组织  mil军事部门  org非盈利组织...

**3.查询方式**

+ 递归查询
 ----------
![icon3](https://img-blog.csdn.net/20140518100201640)


+ 迭代查询
 ----------

![icon4](https://img-blog.csdn.net/20140518100235734)


**4.报文格式**
![icon5](https://jocent.me/wp-content/uploads/2017/06/dns-protocol-format.png)

**5.相关命令**

Windows环境下清空DNS缓存的命令是 ipconfig/flushdns 

也可以通过重启DNS client 和 DHCP client 两项服务清空DNS缓存

Windows环境下可以用命令 ipconfig /displaydns  来查看DNS缓存的内容

nslookup 命令可以用来查看域名对应的IP地址，比如 nslookup jocent.me

参考文章
---
[DNS协议详解及报文格式分析](https://blog.csdn.net/tianxuhong/article/details/74922454)

[DNS协议](https://blog.csdn.net/smilesundream/article/details/69397318)