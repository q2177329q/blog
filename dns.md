书籍2.4
## DNS是
DNS（Domain Name System，域名系统）的主要任务是进行主机名（hostname，也称域名）到 IP 地址转换的目录服务，它由两部分组成：
- 一个由分层的 DNS 服务器实现的分布式数据库
- 一个使得主机能够查询分布式数据库的应用层协议

DNS 服务器通常是运行 BIND（Berkeley Internet Name Domain）软件的 UNIX 机器。DNS 协议运行在 UDP 之上，使用 53 号端口。

## dns服务器分层结构
![image](https://user-images.githubusercontent.com/9465058/155839479-61ee700e-bf51-489c-b072-6f1f6a5aad8f.png)
## DNS 协议

共同实现 DNS 分布式数据库的所有 DNS 服务器存储了资源记录（Resource Record，RR），RR 提供了主机名到 IP 地址的映射。每个 DNS 回答报文包含了一条或多条资源记录。
资源记录是一个包含了下列字段的 4 元组：
```
(Name, Value, Type, TTL)
```

TTL（Time To Live）是该记录的生存时间，它决定了资源记录应当从缓存中删除的时间。Name 和 Value 的值取决于 Type：

- 若 Type = A，则 Name 是主机名，Value 是该主机名对应的 IP 地址。因此，一条类型为 A 的资源记录提供了标准的主机名到 IP 地址的映射。例如 (relay1.bar.foo.com, 145.37.93.126, A) 就是一条类型 A 记录。
- 若 Type = NS，则 Name 是个域（如 foo.com），而 Value 是个知道如何获得该域中主机 IP 地址的权威 DNS 服务器的主机名。这个记录用于沿着查询链来路要 DNS 查询。例如 (foo.com, dns.foo.com, NS) 就是一条类型为 NS 的记录。
- 若 Type = CNAME，则 Value 是别名为 Name 的主机对应的规范主机名。该记录能够向查询的主机提供一个主机名对应的规范主机名，例如 (foo.com, relay1.bar.foo.com, CNAME) 就是一条 CNAME 类型的记录。
- 若 Type = MX，则 Value 是个别名为 Name 的邮件服务器的规范主机名。举例来说，(foo.com, mail.bar.foo.com, MX) 就是一条 MX 记录。MX 记录允许邮件服务器主机名具有简单的别名。值得注意的是，通过使用 MX 记录，一个公司的邮件服务器和其他服务器（如它的 Web 服务器）可以使用相同的别名。为了获得邮件服务器的规范主机名，DNS 客户应当请求一条 MX 记录；而为了获得其他服务器的规范主机名，DNS 客户应当请求 CNAME 记录。


## dns缓存（前端）
1. 浏览器缓存（ttl和dns ttl无关，chrome是1分钟）
2. OS DNS缓存（ttl参考dns ttl）
3. 本地HOSTS文件
4. 路由器缓存
5. 运营商缓存（联通、电信）

## dns-prefetch
手动指定dns预解析
```
<link rel="dns-prefetch" href="//baidu.com">
```

自动解析，https默认没开启
```
// 开启DNS Prefetch
<meta http-equiv="x-dns-prefetch-control" content="on">

// 关闭DNS Prefetch
<meta http-equiv="x-dns-prefetch-control" content="off">
```
浏览器会把dns缓存在系统dns缓存中
