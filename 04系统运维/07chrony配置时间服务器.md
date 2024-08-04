# chrony 配置时间服务器

## 一、测试机同步上游时间服务器

```shell
# 测试机192.168.235.100具有互联网访问权限
[root@localhost ~]# yum install chrony -y
[root@localhost ~]# systemctl enable --now chronyd
[root@localhost ~]# chronyc sources
210 Number of sources = 4
MS Name/IP address         Stratum Poll Reach LastRx Last sample               
===============================================================================
^? tock.ntp.infomaniak.ch        1   6     3     2  +28807s[+28807s] +/-   93ms
^? ntp8.flashdance.cx            2   6     3     2  +28807s[+28807s] +/-  127ms
^? ntp7.flashdance.cx            2   6     3     2  +28807s[+28807s] +/-  128ms
^? time.cloudflare.com           3   6     3     1  +28807s[+28807s] +/-  289ms

* 表示chronyd当前已经同步到的源。
+ 表示可接受的信号源，与选定的信号源组合在一起。
- 表示被合并算法排除的可接受源
? 表示连接已丢失或数据包未通过测试的数据源
x 表示chronyd认为时虚假行情的时钟，即标记该时间与其他多数时间不一致
~ 表示时间似乎具有太多可变性

这时候会发现时间源不可用
-------------------------------------------------------------------------------
vim /etc/chrony.conf
server ntp.aliyun.com iburst            # 配置阿里云时间源服务器为上游时间服务器 iburst 表示加速同步过程

# 将光标定位到 allow 处，将前面的注释删除
# allow 192.168.0.0/16 表示允许哪些地址来同步这台服务器的时间， 如果要允许所有人同步，将网段改成 0.0.0.0/0 即可
# 将光标定位到 local 处，将前面的注释删除
# local stratum 10 # 表示开启手动校准时间功能，如果上游时间服务器故障，客户机也会正常同步这台机器的时间， stratum 表示层数，层数越低，时间来源越精确

# 修改好配置文件后，重启chronyd 服务
[root@localhost ~]# systemctl restart chronyd
[root@localhost ~]# chronyc sources
210 Number of sources = 1
MS Name/IP address         Stratum Poll Reach LastRx Last sample               
===============================================================================
^* 203.107.6.88                  2   6    17    54    +25us[ -735us] +/-   26ms

------------------------------------------------------------------------------------
# 如果开启了防火墙，还需要放行 ntp 服务
firewall-cmd --add-service=ntp --permanent
firewall-cmd --reload
```

## 二、客户机同步测试机的时间

```shell
# 客户机不能访问互联网
yum install chrony -y
systemctl enable --now chronyd
vim /etc/chrony.conf
server 192.168.235.100 iburst
systemctl restart chronyd
```

