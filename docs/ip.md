# 网络层文档
网络层向上提供简单灵活的、无连接的、尽最大努力交付的数据报服务。网络层不用先建立连接，不提供服务质量的承诺。
分组不进行编号，并且所传送的分组有可能丢失、出错、重复和失序，也不保证交付时限。

#### 网络层两种重要的功能：
1. 转发 将分组从路由器的入链路转发到出链路。
2. 路由选择 当分组从发送方流向接收方时，网络层必须决定这些分组所采用的路由或路径。

#### 与 IP 协议配套使用的还有三个协议：
1. 地址解析协议 ARP。
2. 网际控制报文协议 ICMP。
3. 网际组管理协议 IGMP。

#### 将网络互相连接起来的中间设备
1. 物理层使用的中间设备叫做转发器。
2. 数据链路层使用的中间设备叫做网桥或桥接器。
3. 网络层使用的中间设备叫路由器。
4. 在网络层以上使用的中间设备叫网关。

#### IP 地址的编址方法经历了三个阶段
1. 分类的 IP 地址。
2. 子网的划分。
3. 构成超网。

## IP 协议
IP 地址由网络号和主机号组成，它是分等级的地址结构。分等级有两个好处：
1. IP 地址管理机构在分配地址时只分配网络号，主机号由该网络号的单位自行分配，管理方便。
2. 路由器仅根据目的地址的网络号来转发分组，这样可以减少路由表中的项目数。

### 地址分类
A B C 类地址是单播地址（一对一），D类地址为多播地址（一对多），E类地址保留，每一类地址由两个固定长度的字段组成。
1. 网络号，它标志主机或路由器所连接到的网络。
2. 主机号，它标志主机或路由器。
```
IP 地址 = {网络号,主机号}
```
一个网络是指具有相同网络号的主机的集合，因此用转发器或网桥连接起来的若干个网络仍为同一个网络。

注意，近年来已经广泛使用无分类 IP 地址进行路由选择，A B C 类地址的区分已成为历史。

IP 地址中全 0 表示这个（this），网络号字段全 0 的 IP 地址是个保留地址，意思是本网络。

全 0 的主机号字段表示该 IP 地址是本主机所连接到的单个网络地址（5.6.7.8 该主机所在的网络地址就是 5.0.0.0），全 1 的主机号字段表示该网络上的所有主机。

网络号为 127 保留作为本地软件环回测试本主机的进程之间的通信之用。若主机发送一个目的地址为环回地址的 IP 数据报，则不会把数据报发送到任何网络。
网络号为 127 的地址永远不会出现在网络上，因为它不是一个网络地址。

### A 类地址
A 类地址主机号占 3 个字节。最大主机数为 2**24 - 2，A 类地址空间约占整个 IP 地址空间的 50%。
### B 类地址
B 类地址主机号占 2 个字节，最大主机数为 2**16 - 2，B 类地址空间约占整个 IP 地址空间的 25%。
### C 类地址
C 类地址主机号占 1 个字节，最大主机数为 2**8 - 2，C 类地址空间约占整个 IP 地址空间的 12.5%。

### 其他特点
1. IP 地址标志着一台主机（或路由器）和一条链路的接口。
2. 路由器具有两个或以上的 IP 地址。
3. 两个路由器直连的特殊网络通常不分配地址，这样的特殊网络叫无编号网络或无名网络。
4. IP 地址放在 IP 数据报首部，硬件地址（MAC）放在 MAC 帧的首部。
5. IP 数据报中的源和目的地址始终不变，MAC 帧中的源和目的地址在不同的网络上都会变化。