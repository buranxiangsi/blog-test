# URL 包含哪几部分，每部分分别有什么作用

URL = 协议+域名/IP+端口号+路径+查询字符串+锚点

https:// www.baidu.com /s  ?wd=hello&rsv_spt=1 #5
<br>
协议          域名     路径    查询参数          瞄点

## IP的作用是什么，ping 命令怎么用

1. IP (Internet Protocal)
   1. 定位一台设备
   2. 封装数据，跟其他设备交流
   3. 分为内网和外网，由路由器分隔，也叫网关。
   4. 特殊ip
   ```
    127.0.0.1 代表自己
    localhost 通过hosts指定为自己
    0.0.0.0   不表示任何设备

    ping baidu.com
   ```

2. 端口 port
   1. HTTP 80 port
   2. HTTPS 443 port
   3. FTP 21 port
   4. 怎么知道用端口[维基百科查看端口](https://zh.wikipedia.org/wiki/TCP/UDP%E7%AB%AF%E5%8F%A3%E5%88%97%E8%A1%A8#0.E5.88.B01023.E5.8F.B7.E7.AB.AF.E5.8F.A3)
   5. 0-1023 port 给系统使用
   6. 1024 需要管理员权限
   7. http-server 默认 8080 端口
   8. 端口被占用，换另外一个。
3. ip和端口缺一不可。
   
## 域名是什么，分别哪几类域名
1. 域名——ip的别称。
   1. ping baidu.com 得到ip
   2. 一个域名对应不同的ip
   3. 域名和ip通过DNS对应
   4. 请求不同的页面——路径。
   5. 锚点不会传给服务器。
2. 域名的分类
   1. com 顶级域名
   2. xxx.com 一级域名（俗称二级）
   3. www.xxx.com  二级域名 （俗称三级）

# DNS 的作用是什么，nslookup 命令怎么用
1. dns作为将域名和IP地址相互映射的一个分布式数据库，能够使人更方便地访问互联网。使用TCP/UDP port。是域名的核心。
2. nslookup url
3. nslookup用于确定IP地址的域名或域名的IP地址


##  HTTP 协议 TCP/IP
   1. curl 发送HTTP请求
   2. curl -v url
   3. curl -s -v url
   


   



