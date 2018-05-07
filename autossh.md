(顺序从1->2->3，有依赖关系)

成功：
---
1. 初级(7770端口在防火墙中开放与否都可以实现)
    1. a.[SSH反向连接及Autossh - eshizhan - 博客园](https://www.cnblogs.com/eshizhan/archive/2012/07/16/2592902.html)
b.[用啥Ngrok，用SSH解决大局域网反向端口转发问题 - FreeBuf互联网安全新媒体平台 | 关注黑客与极客](http://www.freebuf.com/articles/network/142034.html)
    3. 实现：
a.修改VPS端/etc/ssh/sshd_config加入GatewayPorts yes
b.```ssh -NfR 7770:localhost:22 root@54.37.185.184 -p22```
c.查、杀进程":
```sudo netstat -plant | grep 7770```
```sudo kill -s 9 PID```
d.```ssh victor@localhost -p 7770```


2. 免密码：
    1. 参考：
a. [SSH反向连接及Autossh - eshizhan - 博客园](https://www.cnblogs.com/eshizhan/archive/2012/07/16/2592902.html)
b. [利用ssh传输文件 - jiangyao - 博客园](http://www.cnblogs.com/jiangyao/archive/2011/01/26/1945570.html)
```scp /home/victor/.ssh/id_rsa.pub root@54.37.185.184:/home/share```
1. ```ssh -NfR 7770:localhost:22 root@54.37.185.184 -p22```
2.```autossh -M 5678 -NR 7770:localhost:22 root@54.37.185.184 -p22```(强制退出在本地会留有进程，占用5678端口，需强杀，方法同上)

未尝试(待重启)：
--------

3. 自启动
1.```sudo nano /etc/init.d/autossh```
2.```/bin/su -c '/usr/bin/autossh -M 5678 -NR 7770:localhost:22 root@54.37.185.184 -p22 ' - root```
