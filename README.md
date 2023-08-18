# kuxin
视酷即时通讯前后端源码分享，tg:adoorvip另有酷信全开源新版，更新及二次开发需要m
# **酷信**** 服务端安装部署文档**

目录

[酷信服务端安装部署文档](#_Toc23185) 1

[端口说明](#_Toc23124) 3

[一、 部署方式一直接安装](#_Toc27061) 4

[1) Linux系统下直接安装IM相关服务 4](#_Toc6854)

[1、 安装MongoDB 4](#_Toc2148)

[2、 安装Redis 5](#_Toc8647)

[3、 安装Jdk1.8+ 6](#_Toc16602)

[4、安装RocketMQ队列 7](#_Toc11290)

[5、安装Spring-boot-imapi api 接口服务 11](#_Toc12894)

[6、 安装IM-Server socketIM通讯服务 13](#_Toc9018)

[7、安装 third-push 推送服务 17](#_Toc29345)

[8、安装message-push服务 19](#_Toc22437)

[9、安装Upload文件上传服务 20](#_Toc17242)

[10、安装Nginx，配置文件访问 23](#_Toc12969)

[11、修改后台配置 26](#_Toc1381)

[将服务设置为开机自启动](#_Toc17255) 27

[修改后台配置](#_Toc24109) 34

[web&公众号部署 35](#_Toc26922)

[2) Windows 系统下安装IM 相关服务 39](#_Toc26931)

[1、安装MongoDB 39](#_Toc11594)

[2、安装Redis 40](#_Toc24292)

[3、安装jdk1.8+ 41](#_Toc12579)

[4、安装rocketmq 44](#_Toc9002)

[5、安装Spring-boot-imapi 46](#_Toc30970)

[6、安装运行IMServer 47](#_Toc334)

[7、安装message-push 48](#_Toc25275)

[8、安装third-push 49](#_Toc18472)

[9、安装Upload文件上传服务 49](#_Toc20470)

[10、配置Nginx文件访问 49](#_Toc20667)

[Windows下将服务自启动说明： 50](#_Toc1166)

[IM各服务启动顺序 53](#_Toc2723)

[二、部署方式二（通过](#_Toc2024)docker部署） 56

[1. 安装docker（以centos7.X 为例） 56](#_Toc17666)

[2. Docker 创建Redis 容器 57](#_Toc1189)

[3. Docker 创建Mongodb容器 57](#_Toc24532)

[4. Docker 创建imapi-server容器 58](#_Toc17202)

[5. Docker 创建IMServer容器 59](#_Toc12489)

[6. Docker 创建RocketMq容器 61](#_Toc32165)

[7. Docker 创建third-push容器 62](#_Toc27)

[8.Docker 创建message-push 容器 62](#_Toc32713)

[9.Docker 创建Upload容器 63](#_Toc25856)

[10. Docker 创建Nginx容器 64](#_Toc23622)

[三、配置第三方短信服务](#_Toc18079) 66

[四、配置微信充值与提现](#_Toc2118) 67

[1.配置微信充值 67](#_Toc11695)

[2.配置微信提现 68](#_Toc30983)

[3.配置支付宝相关 71](#_Toc13365)

[五、 推送、地图与](#_Toc31546)Https 域名证书相关申请 71

[1.小米推送 71](#_Toc3058)

[2.华为推送 73](#_Toc31265)

[3.魅族推送 75](#_Toc6531)

[4.vivo推送 77](#_Toc23746)

[5.oppo推送 80](#_Toc20801)

[6.百度地图 82](#_Toc4537)

[7.谷歌推送 84](#_Toc11365)

[8.谷歌地图 87](#_Toc26204)

[9.Https 域名证书 89](#_Toc32757)

[六、 服务器管理、维护](#_Toc27737) 94

[如何连接上服务器以](#_Toc3215)xshell为示例 94

[相关问题排查处理](#_Toc2297) 96

[1. 请求异常,请稍后重试 96](#_Toc5384)

[2. 消息发不出去收不到 , 一直连接中 97](#_Toc25505)

[3. 文件上传异常 99](#_Toc31604)

[4. 群控制消息不推送, 导致禁言失效 或收不到邀请进群通知 99](#_Toc21844)

[Linux常用命令大全 100](#_Toc7965)

[1.修改调整服务器最大连接数 100](#_Toc18746)

[2.查看监听的端口 101](#_Toc19303)

[3.设置防火墙 102](#_Toc16001)

[4.查看日志 103](#_Toc18112)

[5.服务的启动与关闭 104](#_Toc24076)

[6.通过nginx 做端口转发 104](#_Toc18944)

[7.通过(iptables /fireWall)做端口转发 105](#_Toc27337)

[1) 开启服务器的ip 转发功能，默认是关闭的 105](#_Toc11246)

[2） 配置端口转发 106](#_Toc18865)

[说明：将](#_Toc10690)47.75.89.57 的8088 端口 转至 47.91.255.114 下的 5222 端口 106

[8.windows 系统下的端口映射 107](#_Toc1717)

[如何连接上服务器以](#_Toc15576)xshell为示例 108

[相关问题排查处理](#_Toc9769) 110

[5. 请求异常,请稍后重试 110](#_Toc12026)

[6. 消息发不出去收不到 , 一直连接中 111](#_Toc20073)

[7. 文件上传异常 113](#_Toc27108)

[8. 群控制消息不推送, 导致禁言失效 或收不到邀请进群通知 113](#_Toc29647)

[Linux常用命令大全 114](#_Toc9194)

[七、](#_Toc16691)wss配置说明 115

[八、数据库加密、定时备份](#_Toc23285) 116

[1. MongoDB加密说明： 116](#_Toc2443)

[2. Mongodb 数据备份： 117](#_Toc22567)

[3.Redis 加密说明： 117](#_Toc13156)

[九、搭建服务端代码开发环境（以](#_Toc2540)IntelliJ IDEA 2018为例） 118

[前期准备](#_Toc21834) 118

[1. 打开项目 121](#_Toc12096)

[2. 导入下载不到的jar包解决pom报错 124](#_Toc12895)

[3. 编译并运行项目 126](#_Toc26223)

[1.编译打包 126](#_Toc171)

[2.运行 127](#_Toc672)

# 端口说明

| 服务 | 用途 | 使用端口 | 说明 |
| --- | --- | --- | --- |
| Mongodb | 数据库 | 28018 | 不用对外开放 |
| Redis | 缓存 | 6379 | 不用对外开放 |
| Spring-boot-imapi | Api 接口 | 8092 | 需要开放 |
| Im-server | 通讯服务 | Web端使用5260端口，手机端使用5666端口 | 需要开放 |
| Upload | 文件上传 | 8088 | 需要开放 |
| Nginx | 静态文件访问 | 一般使用8089 | 需要开放 |

1.
# 部署方式一直接安装

注: 酷信相关部署文件请使用提供给贵方的,下载服务器上的部署包没维护了

1.
## Linux系统下直接安装IM相关服务

1.
### 安装MongoDB

下载并解压缩mongoDb安装包：

[root@shiku~]# cd /opt

[root@shiku~]# wget [https://fastdl.mongodb.org/linux/mongodb-linux-x86\_64-rhel70-4.2.8.tgz](https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-rhel70-4.2.8.tgz)

[root@shiku~]# tar -zxvf mongodb-linux-x86\_64-rhel70-4.2.8.tgz

[root@shiku~]# mv mongodb-linux-x86\_64-rhel70-4.2.8 mongodb-4.2.8

在/opt/mongodb-4.2.8目录下创建mongo.conf文件内容如下：

[root@shiku~]#cd mongodb-4.2.8

[root@shiku~]#vim mongo.conf

配置模板：

systemLog:

destination: file

path: "/opt/mongodb-4.2.8/logs/mongodb.log"

logAppend: true

storage:

dbPath: "/data/mongodb"

journal:

enabled: true

directoryPerDB: true

wiredTiger:

engineConfig:

configString: cache\_size=2G

directoryForIndexes: true

processManagement:

fork: true

net:

#bindIp: 127.0.0.1

port: 28018

setParameter:

enableLocalhostAuthBypass: false

# 开启授权认证

#security:

# authorization: enabled

然后创建mongodb数据目录，和日志目录

[root@shiku~]# mkdir -p /data/mongodb

[root@shiku~]# mkdir logs

在/opt/mongodb-4.2.8目录下创建start启动脚本内容如下：

/opt/mongodb-4.2.8/bin/mongod --config=/opt/mongodb-4.2.8/mongo.conf

执行start脚本，出现如下图所示内容则启动成功

![Shape1](RackMultipart20230818-1-nx22ha_html_ea3a3072c32491f9.gif) ![](RackMultipart20230818-1-nx22ha_html_c77b816fd733b8cd.png)

Stop脚本：

ps -ef|grep mongo.conf|grep -v grep|awk '{printf $2}'|xargs kill -9

1.
### 安装Redis

#注: redis 端口请勿暴露外网(容易中病毒),如果实在需要暴露请设置好密码并改个端口

下载、解压、安装

[root@shiku~]# cd /opt

[root@shiku~]# wget https://download.redis.io/releases/redis-4.0.1.tar.gz

[root@shiku~]# tar -zxvf redis-4.0.1.tar.gz

[root@shiku~]# cd redis-4.0.1

[root@shiku~]# make && make install

修改/opt/redis-4.0.1目录下redis.conf文件中配置项：

daemonize yes（进程后台运行）

在/opt/redis-4.0.1目录下创建start启动脚本内容如下：

/opt/redis-4.0.1/src/redis-server /opt/redis-4.0.1/redis.conf

执行sh start 命令启动脚本，查看redis是否启动成功

![](RackMultipart20230818-1-nx22ha_html_fbe00337e58a97d5.png)

**Stop**** 脚本：**

ps -ef|grep /opt/redis-4.0.1/src/redis-server|grep -v grep|awk '{printf $2}'|xargs kill -9

ps -ef|grep /opt/redis-4.0.1/src/redis-server

1.
### 安装Jdk1.8+

[root@shiku~]# cd /opt

[root@shiku~]#

下载地址 [https://www.oracle.com/java/technologies/javase/javase8u211-later-archive-downloads.html](https://www.oracle.com/java/technologies/javase/javase8u211-later-archive-downloads.html)

![](RackMultipart20230818-1-nx22ha_html_11956f0e3522a9ea.png)

[root@shiku~]# tar -zxvf jdk-8u251-linux-x64.tar.gz

[root@shiku~]# mkdir java

[root@shiku~]# mv jdk1.8.0\_251 ./java

**设置**** jdk ****环境变量**

这里采用全局设置方法，就是修改etc/profile，它是是所有用户的共用的环境变量

[root@shiku~]# vim /etc/profile

打开之后在末尾添加

JAVA\_HOME=/opt/java/jdk1.8.0\_251

JRE\_HOME=/opt/java/jdk1.8.0\_251/jre

CLASSPATH=.:$JAVA\_HOME/lib/dt.jar:$JAVA\_HOME/lib/tools.jar:$JRE\_HOME/lib

PATH=$JAVA\_HOME/bin:$PATH

export PATH JAVA\_HOME CLASSPATH

使环境变量生效

[root@shiku~]# source /etc/profile

检验是否安装成功

在终端执行： java -version 命令，看看是否安装成功，成功则显示如下

java version "1.8.0\_251"

Java(TM) SE Runtime Environment (build 1.8.0\_251-b08)

Java HotSpot(TM) 64-Bit Server VM (build 25.251-b08, mixed mode)

![](RackMultipart20230818-1-nx22ha_html_d75facf33e3e905e.png)

可能出现的问题：

若出现 bash: /usr/bin/java: /lib/ld-linux.so.2: bad ELF interpreter: No such file or directory

执行：sudo yum install glibc.i686 命令安装glibc

### 4、安装RocketMQ队列

下载地址：https://archive.apache.org/dist/rocketmq/4.7.1/rocketmq-all-4.7.1-bin-release.zip

cd /opt

wgethttps://archive.apache.org/dist/rocketmq/4.7.1/rocketmq-all-4.7.1-bin-release.zip

unzip rocketmq-all-4.7.1-bin-release.zip

mv rocketmq-all-4.7.1-bin-release rocketmq-4.7.1

cd rocketmq-4.7.1

调整rocketMq 的内存值

**注意：这里请根据机器的实际情况进行调整，如机器内存较大可适当配置高一点**

vim bin/runbroker.sh

![](RackMultipart20230818-1-nx22ha_html_1edf8b33bd05ad12.png)

vim bin/runserver.sh

![](RackMultipart20230818-1-nx22ha_html_f93b5fdaa705cc23.png)

vim startSrv

写入如下内容：

nohup sh ./bin/mqnamesrv \> ./logs/rocketmqlogs/namesrv.log &

tail -f ./logs/rocketmqlogs/namesrv.log

执行startSrv 脚本启动nameServer

sh startSrv

可能遇到的问题

![](RackMultipart20230818-1-nx22ha_html_1a900b994c8ba64b.png)

解决办法

mkdir -p ./logs/rocketmqlogs/

\> ./logs/rocketmqlogs/namesrv.log

再次执行 startSrv 脚本启动nameServer

sh startSrv

![](RackMultipart20230818-1-nx22ha_html_d2f03da605229c9d.png)

vim startBroker

写入如下内容：

nohup sh bin/mqbroker -n localhost:9876 \> ./logs/rocketmqlogs/broker.log &

tail -f ./logs/rocketmqlogs/broker.log

执行startBroker脚本启动borker

sh startBroker

![](RackMultipart20230818-1-nx22ha_html_f554e3e3043d336.png)

注意：如果服务器是多网卡的话RocketMQ要绑定一个内网IP

1.打开broker.conf文件

vim conf/broker.conf

2.增加如下两条配置

namesrvAddr = 192.168.0.159:9876

brokerIP1 = 192.168.0.159

![](RackMultipart20230818-1-nx22ha_html_bfb5ad8888ae149c.png)

3.修改startBroker文件

nohup sh bin/mqbroker -c ./conf/broker.conf -nlocalhost:9876 \> ./logs/rocketmqlogs/broker.log &

tail -f ./logs/rocketmqlogs/broker.log

执行jps 命令 查看正常应该能看到NamesrvStaup 和 BrokerStartup

![](RackMultipart20230818-1-nx22ha_html_b2549563ae716592.png)

注册推送消息、用户状态话题

sh bin/mqadmin updateTopic -n localhost:9876 -c DefaultCluster -t pushMessage

sh bin/mqadmin updateTopic -n localhost:9876 -c DefaultCluster -t xmppMessage

sh bin/mqadmin updateTopic -n localhost:9876 -c DefaultCluster -t userStatusMessage

sh bin/mqadmin updateTopic -n localhost:9876 -c DefaultCluster -t HWPushMessage

sh bin/mqadmin updateTopic -n localhost:9876 -c DefaultCluster -t fullPushMessage

sh bin/mqadmin updateTopic -n localhost:9876 -c DefaultCluster -t keywordMessage

![](RackMultipart20230818-1-nx22ha_html_991084b2d16de4eb.png)

附： 单个脚本启动

vim vim mqStart

写入如下内容：

#!/bin/sh

export JAVA\_HOME=/opt/java/jdk1.8.0\_251/

nohup sh /opt/rocketmq-4.7.1/bin/mqnamesrv \> /opt/rocketmq-4.7.1/logs/rocketmqlogs/namesrv.log 2\>&1 &

echo "Start Name Server End"

nohup sh /opt/rocketmq-4.7.1/bin/mqbroker -n localhost:9876 \> /opt/rocketmq-4.7.1/logs/rocketmqlogs/broker.log 2\>&1 &

echo "Start Broker End"

附： 单个脚本停止

vim mqStop

#!/bin/sh

sh /opt/rocketmq-4.7.1/bin/mqshutdown broker &

sh /opt/rocketmq-4.7.1/bin/mqshutdown namesrv

echo "Please wait process to exit! check it type jps"

附：停止命令

sh bin/mqshutdown namesrv

sh bin/mqshutdown broker

### 5、安装Spring-boot-imapi api 接口服务

[root@shiku~]# cd /opt

[root@shiku~]#将提供给贵方的spring-boot-imapi部署文件放到/opt目录中

[root@shiku~]# cd spring-boot-imapi

[root@shiku~]# vim application.properties

2)修改 **application.properties** 配置文件

![](RackMultipart20230818-1-nx22ha_html_be76f931c00a3f1c.png)

![](RackMultipart20230818-1-nx22ha_html_6fb1aa1339fdc773.png)

1. 在spring-boot-imapi目录下执行sh start命令运行imapi接口服务

![](RackMultipart20230818-1-nx22ha_html_b38089cd738042a9.png)

修改后台配置

启动完成后，在浏览器打开链接"http://localhost:8092/console/login",出现如下图所示内容即酷信接口部署成功：

![](RackMultipart20230818-1-nx22ha_html_e344c7c2c26ddb5f.png)

**注：超级管理员账号：**** 1000 **** 初始密码： ****1000**

1.
### 安装IM-Server socketIM通讯服务

#### 6.1 包目录说明

IMServer-聊天服务器

![](RackMultipart20230818-1-nx22ha_html_733d0d67661c1.png)

lib 目录为 jar包存放目录

imserver.properties 为服务器配置文件

[root@shiku~]# cd /opt

[root@shiku~]# 将提供给贵方的IMServer-聊天服务器部署文件放到/opt目录中

[root@shiku~]# cd IMServer

[root@shiku~]# vim imserver.properties

#### 6.2修改imserver.properties 配置文件

![](RackMultipart20230818-1-nx22ha_html_eb8a22c5119b75da.png)

#### 6.3 证书和jar包的放置

1.将server-XXX.dat重命名为server.dat放到IMServer服务目录

![](RackMultipart20230818-1-nx22ha_html_6745c9113b532071.png)

2.在imserver.properties配置文件中进行配置server.dat文件的位置

clusterLicenseDir=/opt/IMServer/server.dat

![](RackMultipart20230818-1-nx22ha_html_3d128151b1bbda6a.png)

3.将server-start-1.3.0.jar和chat-im-common-1.3.0.jar这2个jar包放到IMServer服务目录中的lib目录中

![](RackMultipart20230818-1-nx22ha_html_b22895b0d1c940b2.png)

4.在IMServer服务目录中执行sh start 启动IMServer服务

#### 6.4 JVM、GC设置和建议

修改 start 启动文件

对于非生产部署（开发或说明环境），我们建议使用JVM的默认内存设置（这取决于底层操作系统），这会导致自动内存分配，并且根据经验，这是最安全的。环境。

对于生产环境，我们建议使用固定大小的HEAP - 初始和最大大小，可以分别设置（JVM ）-Xms和-XmxJVM标志

##### 服务器类机器（非VM），\> 16GB，\> = 8核CPU

建议启用CMS垃圾收集器。根据实际物理内存大小调整Xms和Xms大小以获得实际可用内存使用以下内容：

GC="-XX:+UseBiasedLocking -XX:+UseConcMarkSweepGC -XX:+UseParNewGC -XX:NewRatio=2 -XX:+CMSIncrementalMode -XX:-ReduceInitialCardMarks -XX:CMSInitiatingOccupancyFraction=70 -XX:+UseCMSInitiatingOccupancyOnly"

EX="-XX:+OptimizeStringConcat -XX:+DoEscapeAnalysis -XX:+UseNUMA"

#GC\_DEBUG=" -XX:+PrintTenuringDistribution -XX:+PrintGCDetails -XX:+PrintGCDateStamps -XX:+PrintGCTimeStamps -Xloggc:jvm.log -verbose:gc "

HEAP=" -Xms10G -Xmx10G"

JAVA\_OPTIONS="${GC} ${GC\_DEBUG} ${EX} ${HEAP}"

nohup java -Djava.ext.dirs="lib" ${JAVA\_OPTIONS} com.shiku.imserver.IMServerStarter imserver.properties \> log.log &

对于具有大量可用内存的服务器，使用G1GC收集器可能是一个更好的主意：

#osgiEnabled=(true|false)

#osgiEnabled=false

OSGI=${osgiEnabled}

ENC="-Dfile.encoding=UTF-8 -Dsun.jnu.encoding=UTF-8"

GC="-XX:+UseG1GC -XX:ConcGCThreads=4 -XX:G1HeapRegionSize=2 -XX:InitiatingHeapOccupancyPercent=35 -XX:MaxGCPauseMillis=100"

EX="-XX:+OptimizeStringConcat -XX:+DoEscapeAnalysis -XX:+UseNUMA"

#GC\_DEBUG=" -XX:+PrintTenuringDistribution -XX:+PrintGCDetails -XX:+PrintGCDateStamps -XX:+PrintGCTimeStamps -Xloggc:logs/jvm.log -verbose:gc "

HEAP="-Xms60G -Xmx60G"

JAVA\_OPTIONS="${GC} ${GC\_DEBUG} ${EX} ${HEAP}"

nohup java -Djava.ext.dirs="lib" ${JAVA\_OPTIONS} com.shiku.imserver.IMServerStarter imserver.properties \> log.log &

##### 8GB RAM，4核CPU等效

建议启用CMS垃圾收集器。必须配置NewRatio。需要调整Xms和Xms大小以获得实际可用内存。应该使用以下内容：

GC="-XX:+UseBiasedLocking -XX:+UseConcMarkSweepGC -XX:+UseParNewGC -XX:NewRatio=2 -XX:+CMSIncrementalMode -XX:-ReduceInitialCardMarks -XX:CMSInitiatingOccupancyFraction=70 -XX:+UseCMSInitiatingOccupancyOnly"

EX="-XX:+OptimizeStringConcat -XX:+DoEscapeAnalysis -XX:+UseNUMA"

#GC\_DEBUG=" -XX:+PrintTenuringDistribution -XX:+PrintGCDetails -XX:+PrintGCDateStamps -XX:+PrintGCTimeStamps -Xloggc:logs/jvm.log -verbose:gc "

HEAP="-Xms7G -Xmx7G"# heap memory settings must be adjusted on per deployment-base!

JAVA\_OPTIONS="${GC} ${GC\_DEBUG} ${EX} ${HEAP}"

nohup java -Djava.ext.dirs="lib" ${JAVA\_OPTIONS} com.shiku.imserver.IMServerStarter imserver.properties \> log.log &

在IMServer 执行 start 启动 服务

### 7、安装 third-push 推送服务

third-push服务为离线消息推送服务，去消费IM-Server 放到RocketMq 队列里的离线消息

third-push 部署包各个文件说明

![](RackMultipart20230818-1-nx22ha_html_c3ca18ce6edaf5a2.png)

**安装**** third-push **** 推送服务**

[root@shiku~]# cd /opt

将提供给贵方的third-push部署文件放到/opt目录中

[root@shiku~]# cd third-push

[root@shiku~]# vim application.properties

修改application.properties 配置文件

![](RackMultipart20230818-1-nx22ha_html_3606571961824bfc.png)

目前ios 支持anps和极光推送 ，安卓目前集成了华为、小米、魅族、vivo、oppo，谷歌六种推送，如果手机有谷歌框架且能访问外网，会使用谷歌推送，否则根据机型来，非以上机型使用小米推送

如已经申请好相关配置，将申请好的小米、华为、极光 等平台的key secret 配置到对应的位置。也可以后续在配置，加上配置重启third-push 服务即可

![](RackMultipart20230818-1-nx22ha_html_31e31314733433a3.png)

ios apns 推送配置

替换ios apns推送证书，个人版和企业版 **选择一个使用** 即可，需要注意在申请ios apns 证书的时候 **必须要设置密码** 。

3.修改完配置后使用 sh start 命令启动third-push服务

### 8、安装message-push服务

说明： Message-push 是从 imapi 中独立出来的服务，用于发送系统Xmpp 消息

Imapi 服务里面群组等部分接口操作后，需要发一条xmpp 消息通知用户，

此时imapi 将需要发送的xmpp 消息放到rocketMq 队列下，由Message-push 服务获取队列里的消息然后把消息经过IMServer 发送到设备端

[root@shiku~]# cd /opt

将提供给贵方的message-push部署文件放到/opt目录中

[root@shiku~]# cd message-push

[root@shiku~]# vim application.properties

参照如下示例，修改配置文件

![](RackMultipart20230818-1-nx22ha_html_eedf04d30f149a9c.png)

启动 message-push 服务

[root@shiku~]#sh start

### 9、安装Upload文件上传服务

[root@shiku~]# cd /opt

将提供给贵方的upload部署文件放到/opt目录中

[root@shiku~]# cd upload

[root@shiku~]# vim application.properties

2）参照如下示例修改配置：

说明：/data/www/resources：文件上传成功后存储的根目录

beginIndex：根目录"/data/www/resources"的字符串长度（从0开始）用于分隔字符串生成文件链接用（需要注意，如果修改了相关路径，beginIndex 的数值也要相应修改）

![](RackMultipart20230818-1-nx22ha_html_b236885103dc3c28.png)

![](RackMultipart20230818-1-nx22ha_html_6c956b62733b4138.png)

需要在upload服务application.properties配置文件最后位置进行添加下面信息，如果存在可以不用添加

# bean 名称冲突时允许覆盖

spring.main.allow-bean-definition-overriding=true

# 字段为空不进行序列化

spring.jackson.default-property-inclusion=non\_null

## springboot文件上传配置

spring.servlet.multipart.enabled=true

spring.servlet.multipart.max-file-size=1024MB

spring.servlet.multipart.max-request-size=10240MB

spring.servlet.multipart.file-size-threshold=1024KB

spring.servlet.multipart.location=/opt

server.tomcat.max-http-post-size=-1

3）在文件上传服务所在机器创建存储目录（例如"/data/www/resources"）并初始化目录结构

可以直接将以下命令全部拷贝到Linux服务器一次性执行

mkdir -p /data/www/resources

cd /data/www/resources

mkdir audio

mkdir avatar

mkdir avatar/o

mkdir avatar/t

mkdir avatar\_r

mkdir avatar\_r/o

mkdir avatar\_r/t

mkdir gift

mkdir image

mkdir image/o

mkdir image/t

mkdir other

mkdir preview

mkdir temp

mkdir u

mkdir music

mkdir music/music

mkdir music/mPhoto

mkdir video

4） 启动 upload

[root@shiku~]# Cd /opt/upload

[root@shiku~]# sh start

![](RackMultipart20230818-1-nx22ha_html_61732c4d3d8d9833.png)

文件上传测试页面访问 ip:8088

![](RackMultipart20230818-1-nx22ha_html_bcc4f20256c41aa3.png)

### 10、安装Nginx，配置文件访问

**首先安装**  **nginx**  **所需的依赖**

[root@shiku~]# yum install -y pcre pcre-devel zlib zlib-devel openssl openssl-devel

**安装**  **Nginx-1.9.11**

[root@shiku~]# cd /opt

[root@shiku~]# wget http://distfiles.macports.org/nginx/nginx-1.9.11.tar.gz

[root@shiku~]# tar -zxvf nginx-1.9.11.tar.gz

[root@shiku~]# mv nginx-1.9.11 nginx-install

[root@shiku~]# cd nginx-install

[root@shiku~]# ./configure --prefix=/opt/nginx-1.9.11 --with-http\_ssl\_module --with-stream

[root@shiku~]# make && make install

[root@shiku~]# rm -rf ../nginx-install

在/opt/nginx-1.9.11目录下创建start、stop脚本：

start脚本： vim start ，写入如下内容

./sbin/nginx

ps -ef|grep nginx

stop脚本： vim stop 写入如下内容

./sbin/nginx -s stop

ps -ef|grep nginx

1） 首先请确保已经安装 Nginx，如没有安装请参考上面的 " **安装**  **Nginx-1.9.11**

"中的步骤进行安装。

1. **在**** upload **** 所在的机器上** 配置头像访问

说明：由于FastDfs 不支持对上传文件的自定义命名，而目前用户头像是根据userId 命名的，所以目前用户头像没有使用FastDfs 储存。

修改Nginx 配置文件 nginx.conf ，添加如下内容（ **域名配置示例** ）

#用户头像访问

server{

listen 80;

server\_name head.shiku.co;

#拒接访问html 等类型的文件避免受到脚本攻击

location ~\* /\.(html|htm|jsp|php|js)$ {

deny all;

}

location /{

root /data/www/resources;

expires 4d;

}

}

（ **ip**  **配置示例** ）

server{

listen 8089;

#本机外网ip

server\_name 192.168.0.168;

#拒接访问html 等类型的文件避免受到脚本攻击

location ~ /\.(html|htm|jsp) {

deny all;

}

location ~\* /{

root /data/www/resources;

expires 4d;

}

}

如按IP方式配置即得到文件访问、下载路径 为 ip:8089

3) 执行start、stop脚本，查看nginx是否启动、停止成功：

![](RackMultipart20230818-1-nx22ha_html_db68413b5dbd2884.png)

### 11、修改后台配置

Imapi服务启动完成后，在浏览器打开链接"http://localhost:8092/console/login"

账号密码 默认1000

将系统配置---\> 客户端配置里的地址修改为部署的服务器的地址，这些地址用于在客户端启动时返回给客户端使用，请参考下图

![](RackMultipart20230818-1-nx22ha_html_98657470eae2b7ae.png)

修改配置保存后访问

[http://localhost:8092/config](http://localhost:8092/config)

![](RackMultipart20230818-1-nx22ha_html_781afa49f3727bc2.png)

最后

[http://localhost:8092/config](http://localhost:8092/config)为客户端配置的apiurl 将 apiurl和 apikey（在imapi服务配置文件中配置） 提供 给客户端，客户端打包需要的，至此大功告成。

### 将服务设置为开机自启动

**注意：这里的启、停本质上也是执行对应服务的安装目录下的**** start **** 与 ****stop**** 脚本**

**如果之前**** start ****脚本里配置的是相对路径，那么就需要改为绝对路径**

1.
#### Mongodb

在/lib/systemd/system/目录下新建mongodb.service文件，内容如下：

[Unit]

Description=mongodb

After=network.target remote-fs.target nss-lookup.target

[Service]

Type=forking

ExecStart=/opt/mongodb-3.2.4/bin/mongod --config /opt/mongodb-3.2.4/mongo.conf

ExecReload=/bin/kill -s HUP $MAINPID

ExecStop=/opt/mongodb-3.2.4/bin/mongod --shutdown --config /opt/mongodb-3.2.4/mongo.conf

PrivateTmp=true

[Install]

WantedBy=multi-user.target

如图所示：

![](RackMultipart20230818-1-nx22ha_html_e27aa0bb19593f7b.png)

#设置权限

[root@shiku~]# chmod 754 mongodb.service

#启动服务

[root@shiku~]#systemctl start mongodb.service

#关闭服务

[root@shiku~]#systemctl stop mongodb.service

#开机启动

[root@shiku~]#systemctl enable mongodb.service

1.
#### Redis

在/lib/systemd/system/目录下新建redis.service文件，内容如下：

[Unit]

Description=redis

After=syslog.target network.target

[Service]

Type=forking

PIDFile=/var/run/redis\_6388.pid

ExecStart=/opt/redis-4.0.1/src/redis-server /opt/redis-4.0.1/redis.conf

ExecReload=/bin/kill -USR2 $MAINPID

ExecStop=/bin/kill -SIGINT $MAINPID

[Install]

WantedBy=multi-user.target

如下图所示：

![](RackMultipart20230818-1-nx22ha_html_2dcc9c6923d0121b.png)

#设置权限

[root@shiku~]# chmod 754 redis.service

#启动服务

[root@shiku~]#systemctl  start  redis.service

#关闭服务

[root@shiku~]#systemctl  stop  redis.service

#开机启动

[root@shiku~]#systemctl  enable  redis.service

1.
#### Nginx

在/lib/systemd/system/目录下新建 nginx.service文件，内容如下：

[Unit]

Description=nginx

After=syslog.target network.target

[Service]

Type=forking

ExecStart=/opt/nginx\_1.7.9/sbin/nginx

ExecReload=/opt/nginx\_1.7.9/sbin/nginx -s reload

ExecStop=/opt/nginx\_1.7.9/sbin/nginx -s quit

PrivateTmp=true

[Install]

WantedBy=multi-user.target

如下图所示：

![](RackMultipart20230818-1-nx22ha_html_6f142839aef24251.png)

#设置权限

[root@shiku~]# chmod 754 nginx.service

#启动服务

[root@shiku~]#systemctl  start  nginx.service

#关闭服务

[root@shiku~]#systemctl  stop  nginx.service

#开机启动

[root@shiku~]#systemctl  enable  nginx.service

1.
#### Spring-boot-imapi

注: 设置开机自启动服务启动脚本全部要求使用绝对路径 ，和给予相应执行权限

如 ：

![](RackMultipart20230818-1-nx22ha_html_c8f2ea4f9076f6ae.png)

在/lib/systemd/system/目录下新建 imapi.service文件，内容如下：

[Unit]

Description=imapi

After=syslog.target network.target remote-fs.target nss-lookup.target mongodb.service redis.service

[Service]

Type=simple

PIDFile=/opt/spring-boot-imapi/imapi.pid

ExecStart=/opt/spring-boot-imapi/start

ExecReload=/bin/kill-s HUP $MAINPID

ExecStop=/opt/spring-boot-imapi/stop

PrivateTmp=true

#SuccessExitStatus=143

[Install]

WantedBy=multi-user.target

如下图所示：

![](RackMultipart20230818-1-nx22ha_html_5dad5119049a342b.png)

#设置权限

[root@shiku~]# chmod 754 imapi.service

#启动服务

[root@shiku~]#systemctl  start  imapi.service

#关闭服务

[root@shiku~]#systemctl  stop  imapi.service

#开机启动

[root@shiku~]#systemctl  enable  imapi.service

1.
#### IMServer

在/lib/systemd/system/目录下新建 imserver.service文件，内容如下：

[Unit]

Description=imserver

After=syslog.target network.target remote-fs.target nss-lookup.target mongodb.service redis.service

[Service]

Type=forking

ExecStart=/opt/IMServer/start

ExecReload=/bin/kill-s HUP $MAINPID

ExecStop=/opt/IMServer/scripts/tigase.sh stop /opt/IMServer/stop

PrivateTmp=true

[Install]

WantedBy=multi-user.target

#设置权限

[root@shiku~]# chmod  754  imserver.service

#启动服务

[root@shiku~]# systemctl  start  imserver.service

#关闭服务

[root@shiku~]# systemctl  stop  imserver.service

#开机启动

[root@shiku~]# systemctl  enable  imserver.service

#### 7）rocketmq

在/lib/systemd/system/目录下新建 rocketmq-4.3.2.service文件，内容如下：

[Unit]

Description=rocketmq-4.3.2

After=syslog.target network.target remote-fs.target nss-lookup.target

[Service]

Type=forking

ExecStart=/opt/rocketmq-all-4.3.2-bin-release/mqStart

ExecReload=/bin/kill-s HUP $MAINPID

ExecStop=/opt/rocketmq-all-4.3.2-bin-release/mqStop

PrivateTmp=true

[Install]

WantedBy=multi-user.target

#设置权限

[root@shiku~]# chmod  754  rocketmq-4.3.2.service

#启动服务

[root@shiku~]# systemctl  start  rocketmq-4.3.2.service

#关闭服务

[root@shiku~]# systemctl  stop  rocketmq-4.3.2.service

#开机启动

[root@shiku~]# systemctl  enable  rocketmq-4.3.2.service

#### 8）third-push

在/lib/systemd/system/目录下新建 third-push.service文件，内容如下：

[Unit]

iDescription=third-push

After=syslog.target network.target remote-fs.target nss-lookup.target mongodb.service redis.service rocketmq-4.3.2.service

[Service]

ExecStart=/opt/third-push/start

ExecReload=/bin/kill-s HUP $MAINPID

ExecStop=/opt/third-push/stop

PrivateTmp=true

[Install]

WantedBy=multi-user.target

#设置权限

[root@shiku~]# chmod  754  third-push.service

#启动服务

[root@shiku~]# systemctl  start third-push.service

#关闭服务

[root@shiku~]# systemctl  stop   third-push.service

#开机启动

[root@shiku~]# systemctl  enable   third-push.service

#### 9）message-push

在/lib/systemd/system/目录下新建 message-push.service文件，内容如下：

[Unit]

iDescription=message-push

After=syslog.target network.target remote-fs.target nss-lookup.target mongodb.service redis.service rocketmq-4.3.2.service

[Service]

ExecStart=/opt/message-push/start

ExecReload=/bin/kill-s HUP $MAINPID

ExecStop=/opt/message-push/stop

PrivateTmp=true

[Install]

WantedBy=multi-user.target

#设置权限

[root@shiku~]# chmod  754  message-push.service

#启动服务

[root@shiku~]# systemctl  start  message-push.service

#关闭服务

[root@shiku~]# systemctl  stop   message-push.service

#开机启动

[root@shiku~]# systemctl  enable   message-push.service

#### 10）upload

在/lib/systemd/system/目录下新建 upload.service文件，内容如下：

[Unit]

Description=upload

After=syslog.target network.target remote-fs.target nss-lookup.target mongodb.service redis.service

[Service]

ExecStart=/opt/upload/start

ExecReload=/bin/kill-s HUP $MAINPID

ExecStop=/opt/upload/stop

PrivateTmp=true

[Install]

WantedBy=multi-user.target

#设置权限

[root@shiku~]# chmod  754  upload.service

#启动服务

[root@shiku~]# systemctl  start  upload.service

#关闭服务

[root@shiku~]# systemctl  stop   upload.service

#开机启动

[root@shiku~]# systemctl  enable   upload.service

### 修改后台配置

Imapi服务启动完成后，在浏览器打开链接"http://localhost:8092/console/login"

账号密码 默认1000

将系统配置---\> 客户端配置里的地址修改为部署的服务器的地址，这些地址用于在客户端启动时返回给客户端使用，请参考下图

![](RackMultipart20230818-1-nx22ha_html_912cba186421fb29.png)

修改配置保存后访问

[http://localhost:8092/config](http://localhost:8092/config)

![](RackMultipart20230818-1-nx22ha_html_781afa49f3727bc2.png)

最后

[http://localhost:8092/config](http://localhost:8092/config)为客户端配置的apiurl 将 apiurl和 apikey（在imapi服务配置文件中配置） 提供 给客户端，客户端打包需要的，至此大功告成。

### web&公众号部署

如果未购买该模块可忽略

需要通过WEB 电脑网页端代码进行生成WEB 电脑网页端部署包

将WEB 电脑网页端部署包放到/data/www目录

修改Nginx 配置文件映射目录

server {

listen 80;

server\_name web.xxx.co; #web版访问域名或ip

location / {

root /data/www/kxwebim;

index index.html index.htm;

}

}

目录结构

![](RackMultipart20230818-1-nx22ha_html_eb035b7c16edec04.png)

公众号部署

将部署包上传服务器

如：

![](RackMultipart20230818-1-nx22ha_html_908e120237c62b24.png)

修改配置文件 .properties

![](RackMultipart20230818-1-nx22ha_html_540a395043767bce.png)

![](RackMultipart20230818-1-nx22ha_html_c71b07114ea75cea.png)

修改好配置启动

sh start

修改Nginx 配置

server{

listen 8092;

server\_name imapi.xxx.com; #imapi所处机器外网ip或端口

location /mp{

proxy\_set\_header X-Real-IP $remote\_addr;

proxy\_set\_header X-Forwarded-For $proxy\_add\_x\_forwarded\_for;

proxy\_pass http://127.0.0.1:8096; #mp-server端口

}

location /public{

proxy\_set\_header X-Real-IP $remote\_addr;

proxy\_set\_header X-Forwarded-For $proxy\_add\_x\_forwarded\_for;

proxy\_pass http://127.0.0.1:8096; #mp-server端口

}

location / {

proxy\_set\_header X-Real-IP $remote\_addr;

proxy\_set\_header X-Forwarded-For $proxy\_add\_x\_forwarded\_for;

proxy\_pass http://127.0.0.1:8095; #imapi端口

}

}

1.
## Windows 系统下安装IM 相关服务

### 1、安装MongoDB

下载Windowns版MongoDB [https://fastdl.mongodb.org/win32/mongodb-win32-x86\_64-3.0.7.zip](https://fastdl.mongodb.org/win32/mongodb-win32-x86_64-3.0.7.zip)

解压mongodb-win32-x86\_64-3.0.7.zip并打开mongodb-win32-x86\_64-3.0.7目录

将mongodb-win32-x86\_64-3.0.7目录重命名为mongodb，并在该目录下创建 data/db目录

在mongodb/bin目录下按住Shift键，右键打开菜单，点击 **在此处打开命令窗口** 输入如下命令启动mongodb：

mongod --dbpath E:\IM\mongodb\data\db

出现以下内容表示启动成功

![](RackMultipart20230818-1-nx22ha_html_1019b4b85eb0fb93.png)

### 2、安装Redis

下载Windows版本Redis

[https://github.com/MSOpenTech/redis/releases/download/win-2.8.2104/Redis-x64-2.8.2104.zip](https://github.com/MSOpenTech/redis/releases/download/win-2.8.2104/Redis-x64-2.8.2104.zip)

解压Redis-x64-2.8.2104.zip并打开Redis-x64-2.8.2104目录，在目录按住Shift键，右键

打开菜单，点击 **在此处打开命令窗口** 输入如下命令启动redis：

redis-server.exe redis.windows.conf

或者redis-server.exe redis.windows.conf --maxheap 200m

出现如下图所示的内容说明redis启动成功

![](RackMultipart20230818-1-nx22ha_html_c5c84603340c5f2.png)

### 3、安装jdk1.8+

首先到官网下载 jdk-8u144-windows-x64.exe

[http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)

下载完成后点击进行安装

![](RackMultipart20230818-1-nx22ha_html_1b83fe685c263356.png)

配置环境变量

![](RackMultipart20230818-1-nx22ha_html_b277b6c2974b29d1.png)

![](RackMultipart20230818-1-nx22ha_html_a550a865a9ea574e.png)

在新弹出窗口上，点系统变量区域下面的新建按钮，弹出新建窗口，变量名为JAVA\_HOME，变量值填JDK安装的最终路径，我这里装的地址是D:\Program Files\Java\jdk1.7.0\_51，所以填D:\Program Files\Java\jdk1.7.0\_51，点确定完成。

![](RackMultipart20230818-1-nx22ha_html_55196e26af86c3f4.png)

下面需要设置Path变量，由于系统本身已经存在这个变量，所以无需新建，在原本基本上添加JDK相关的，找到Path变量双击编辑，由于每个值之间用;符号间断，所以先在末尾加上;（注意是英文格式的，不要输其他符号空格等），加上;符号后在末尾加入%JAVA\_HOME%\bin;%JAVA\_HOME%\jre\bin，点确定完成。

![](RackMultipart20230818-1-nx22ha_html_d454ad917b3ef68f.png)

验证安装是否成功

打开windows 命令窗口 输入 java -version 显示如下内容这说明安装成功。

![](RackMultipart20230818-1-nx22ha_html_ada4366d622c9e11.png)

### 4、安装rocketmq

安装前的准备

RocketMQ需要64位的JDK，请确保是64位系统并安装的是的64位JDK。

注: jdk安装路径不能有空格

下载文件：https://archive.apache.org/dist/rocketmq/4.3.2/rocketmq-all-4.3.2-bin-release.zip

安装过程

设置环境变量

变量名：ROCKETMQ\_HOME

变量值：D:\AppData\rocketmq-all-4.3.2-bin-release

![](RackMultipart20230818-1-nx22ha_html_72178e76ebfeeb66.png)

启动NameServer

进入rocketmq的bin文件夹，按着Shift键右击鼠标打开命令窗口，然后执行：start mqnamesrv.cmd

![](RackMultipart20230818-1-nx22ha_html_72cc42ee89949e14.png)

启动完成：

![](RackMultipart20230818-1-nx22ha_html_446a2f68b8253761.png)

注意：此时弹出的窗口不可以关闭。

启动Broker

在刚才的命令窗口继续执行：start mqbroker.cmd -n 127.0.0.1:9876 autoCreateTopicEnable=true，

启动成功：

![](RackMultipart20230818-1-nx22ha_html_5739ce998eb27faa.png)

注意：此时弹出的窗口也不可以关闭。

### 5、安装Spring-boot-imapi

打开酷聊服务端-Windows-Final 目录下的spring-boot-imapi文件夹

![Shape2](RackMultipart20230818-1-nx22ha_html_486ca5d3c16f1e11.gif) ![](RackMultipart20230818-1-nx22ha_html_4aaa31983da8ee3d.png) ![](RackMultipart20230818-1-nx22ha_html_c4df2e11c3f56379.png)

参照Linux安装步骤中的第歩修改 **application.properties** 配置文件

![](RackMultipart20230818-1-nx22ha_html_8e9a7097092d6a92.png)

右键执行start.bat脚本，即可启动imapi

![](RackMultipart20230818-1-nx22ha_html_e8cebc6b9d3d8997.png)

执行脚本后会出现如下窗口，表示启动成功

![](RackMultipart20230818-1-nx22ha_html_8e58c5084ca59b84.png)

### 6、安装运行IMServer

酷信即时通讯服务端找到 IMServer-聊天服务器

![](RackMultipart20230818-1-nx22ha_html_3aecabdd125814e8.png)

参考

参照Linux安装步骤中的第6歩修改 imserver.properties

右键执行start.bat脚本，即可启动IMServer

![](RackMultipart20230818-1-nx22ha_html_b4fd643c0e7b3aa8.png)

![](RackMultipart20230818-1-nx22ha_html_47b620735ce1ece6.png)

出现上述内容 目录下的 log.log 也没有异常 即启动成功

### 7、安装message-push

打开酷聊服务端-Windows-Final 目录下的message-push文件夹

参照Linux安装步骤中的第歩修改 **application.properties** 配置文件

![](RackMultipart20230818-1-nx22ha_html_8e9a7097092d6a92.png)

右键执行start.bat脚本，即可启动message-push

![](RackMultipart20230818-1-nx22ha_html_e8cebc6b9d3d8997.png)

### 8、安装third-push

打开酷聊服务端-Windows-Final 目录下的third-push文件夹

参照Linux安装步骤中的第歩修改 **application.properties** 配置文件

![](RackMultipart20230818-1-nx22ha_html_8e9a7097092d6a92.png)

右键执行start.bat脚本，即可启动third-push

![](RackMultipart20230818-1-nx22ha_html_e8cebc6b9d3d8997.png)

### 9、安装Upload文件上传服务

请参看 linux 下 Upload 安装步骤

### 10、配置Nginx文件访问

打开[http://nginx.org/download/nginx-1.9.11.zip](http://nginx.org/download/nginx-1.9.6.zip)下载并解压，按照Linux安装步骤下"修改配置文件（nginx-1.9.11/conf/nginx.conf）"步骤修改配置，然后双击nginx-1.9.6目录下nginx.exe启动nginx

### Windows下将服务自启动说明：

![](RackMultipart20230818-1-nx22ha_html_97e766ee24e3f97.png)

#### 1.找到此压缩包解压：

![](RackMultipart20230818-1-nx22ha_html_21dcf2933279dad9.png)

解压后会有一个IMStart\_BAT 文件夹,和一个IMAllStart脚本，

其中IMAllStart.bat脚本是总启动脚本，执行后会将所有的IM

相关服务启动，IMStart\_BAT文件夹下存放的是IM的各个分程序的启动脚本，如下图：

![](RackMultipart20230818-1-nx22ha_html_8ed7dcae47363d5d.png)

1.
#### 修改路径

选中上图的脚本，右键 ——》编辑，根据自己的安装位置修改脚本文件中的盘符路径

编辑FreeSwitchStart.bat 脚本，将红线框出的部分修改为自己的FreeSWITCH安装路径

![](RackMultipart20230818-1-nx22ha_html_1a7909a4d89ea480.png)

编辑mongoStart.bat 脚本，将红线框出的部分修改为自己的mongoDB安装路径

![](RackMultipart20230818-1-nx22ha_html_f9cb627ae3c6ba6b.png)

注：这里的mongodb目录下的 data\db 目录是自己创建的，安装步骤中有相应说明。

编辑nginxStart.bat 脚本，将红线框出的部分修改为自己的Nginx安装路径

![](RackMultipart20230818-1-nx22ha_html_a902d6a31ba1d104.png)

编辑redisStart.bat 脚本，将红线框出的部分修改为自己的Redis安装路径

![](RackMultipart20230818-1-nx22ha_html_f9b5842174d4ab3b.png)

编辑spring.bat 脚本，将红线框出的部分修改为自己的Spring-boot-imapi项目的解压路径

![](RackMultipart20230818-1-nx22ha_html_2d03738850443577.png)

编辑tigase.bat 脚本，将红线框出的部分修改为自己的tigase-server项目的解压路径

![](RackMultipart20230818-1-nx22ha_html_97b19b6765597816.png)

编辑tomcat.bat 脚本，将红线框出的部分修改为自己的Tomcat安装路径

![](RackMultipart20230818-1-nx22ha_html_542cd7c77ee0fb64.png)

1.
#### 一键启动

在 ![](RackMultipart20230818-1-nx22ha_html_6d57a90a85e5795d.png) 将IMStart\_BAT 文件夹中所有脚本的路径都修改、保存好之后将IMStart\_BAT 文件夹拷贝到E盘，然后双击执行IMAllStart.bat脚本，即可实现IM相关服务一键启动。

1.
#### 实现开机后IM相关服务自行启动

来到Windows开机启动项目录：

C:\Users\Administrator\AppData\Roaming\Microsoft\Windows\Start Menu\Programs

将MAllStart.bat脚本拷贝到该目录中即可实现开机自启动。

![](RackMultipart20230818-1-nx22ha_html_b72a136d85816035.png)

## IM各服务启动顺序

1.
#### mongoDB 启动

cd /opt/mongodb

执行start脚本，出现如下图所示内容则启动成功

![](RackMultipart20230818-1-nx22ha_html_c77b816fd733b8cd.png)

#### 2 .redis 启动

cd /opt/redis-4.0.1

执行sh start 命令启动脚本，查看redis是否启动成功

![](RackMultipart20230818-1-nx22ha_html_fbe00337e58a97d5.png)

#### 3.roketmq 启动

cd /opt/rocketmq-all-4.3.2-bin-release

执行startSrv 脚本启动nameServer

![](RackMultipart20230818-1-nx22ha_html_d2f03da605229c9d.png)

Ctrl+C

执行startBroker脚本启动borker

![](RackMultipart20230818-1-nx22ha_html_f554e3e3043d336.png)

Ctrl+C

附：停止命令

sh bin/mqshutdown namesrv

sh bin/mqshutdown broker

#### 4.imapi 启动

cd /opt/spring-boot-imapi

在spring-boot-imapi目录下执行sh start命令运行imapi接口服务

![](RackMultipart20230818-1-nx22ha_html_b38089cd738042a9.png)

1.
#### IMServer启动

cd /opt/IMServer

在IMServer目录下执行 sh start 命令启动

1.
#### third-push 启动

cd /opt/third-push

在third-push目录下执行 sh start 命令启动

#### 7.message-push 启动

cd /opt/message-push

在message-push目录下执行 sh start 命令启动

#### 8.nginx-1.9.11 启动

cd /opt/nginx-1.9.11

在nginx-1.9.11目录下执行 sh start 命令启动

1.
#### upload 启动

cd /opt/upload

在upload 目录下执行 sh start 命令启动

# 二、部署方式二（通过docker部署）

注：如习惯使用Docker 容器部署项目，并具有相应的使用、维护经验，则可以使用Docker 容器的方式部署。

1.
## 安装docker（以centos7.X 为例）

**注：**** Docker **** 要求 **** CentOS **** 系统的内核版本高于 **** 3.10 **** ， ****通过**  **uname -r**  **命令查看你当前的内核版本**** 验证你的 ****CentOS**  **版本是否支持**  **Docker**  **。**

[root@shiku ~]# uname -r

![](RackMultipart20230818-1-nx22ha_html_a9d36920486cb858.png)

安装 docker 服务

[root@shiku ~]# yum -y install docker-io

![](RackMultipart20230818-1-nx22ha_html_65040c44e5979877.png)

启动docker 服务

[root@shiku ~]#service docker start

![](RackMultipart20230818-1-nx22ha_html_183c42e4debfbc99.png)

1.
## Docker 创建Redis 容器

**1**** 、从官方仓库拉取 ****redis 4.0.1**  **的镜像**

[root@shiku ~]# docker pull redis:4.0.1

![](RackMultipart20230818-1-nx22ha_html_40908122465548f6.png)

**2**** 、在宿主机创建 **** /data/redis **** 目录**

mkdir /data/redis

**3**** 、通过镜像启动容器**

docker run -p 6388:6379 --name redis-4.0.1 --hostname redis --restart=always -v /data/redis:/data -d redis:4.0.1 redis-server --appendonly yes

![](RackMultipart20230818-1-nx22ha_html_b41793d7ad50cfa7.png)

1.
## Docker 创建Mongodb容器

**1**** 、使用命令从官方仓库拉取 ****3.4.0**  **版本的镜像**

[root@shiku ~]# docker pull mongo:3.4.0

**2**** 、在宿主机创建目录**

mkdir -p /data/mongodb/db

**3**** 、使用镜像启动容器**

docker run -d -p 28018:27017 -v /data/mongodb/db:/data/db --restart=always --name mongodb mongo:3.4.0

**注：**** IP ****地址请根据实际部署机器的内网**** ip ****进行调整**

1.
## Docker 创建imapi-server容器

**1**** 、在 ****imapi**  **的部署文件**** spring-boot-imapi ****中创建**  **imapi\_dockerfile**** 文件 ，写入如下内容**

FROM java:8

VOLUME /opt/logs

COPY application.properties /opt/application.properties

ADD mianshi-im-api-0.0.1-SNAPSHOT.war /opt/mianshi-im-api-0.0.1-SNAPSHOT.war

RUN bash -c 'touch /opt/mianshi-im-api-0.0.1-SNAPSHOT.war'

EXPOSE 8092

ENTRYPOINT ["java","-jar","/opt/mianshi-im-api-0.0.1-SNAPSHOT.war","--spring.config.location=/opt/application.properties"]

**说明：** 这里的application.properties 从 conf\_file/imapi 目录里拷贝，conf\_file 下载地址：

[http://47.75.89.57/soft/conf\_file.tar](http://121.201.67.65/soft/conf_file.tar)

mianshi-im-api-0.0.1-SNAPSHOT.war 为imapi 服务的部署包

**2**** 、通过 ****dockerfile**  **文件构建镜像**

docker build -t imapi -f imapi\_dockerfile ./

![](RackMultipart20230818-1-nx22ha_html_c28b6768138fd213.png)

**3**** 、通过镜像启动容器**

docker run -d -p 8092:8092 -e "UPLOAD\_ADDR=192.168.0.152:8088" -e "MONGODB\_ADDR=192.168.0.151:28018" -e "NAMESRV\_ADDR=192.168.0.155:9876" -e "XMPP\_HOST=192.168.0.155" -e "XMPP\_SERVERNAME=im.shiku.co" -e "REDIS\_ADDR=redis://192.168.0.155:6388" --name imapi-server imapi

1.
## Docker 创建IMServer容器

1. **修改**  **imserver.properties**  **配置文件**

![](RackMultipart20230818-1-nx22ha_html_eb8a22c5119b75da.png)

**3**** 、编辑 ****imserver\_dockerfile**  **文件，写入如下内容：**

**（说明：**** IMServer **** 为 ****部署文件的目录**  **）**

注：5666端口用于Android、Ios、PC 等客户端连接使用，5260 端口用于WEB 版连接使用，如没有 WEB 版5260 端口可不用

FROM java:8

VOLUME /opt/logs

ADD /opt/IMServer/ /opt/IMServer

RUN chmod -R 755 /opt

EXPOSE 5666

EXPOSE 5260

ENTRYPOINT cd /opt/IMServer; java -version; sh start; wait $!

1. **通过**** dockerfile **** 文件构建镜像**

docker build -t imserver -f imserver\_dockerfile ./

**5**** 、通过镜像启动容器**

docker run -d -p 5666:5666 -p 5260:5260 --name IMServer imserver

1.
## Docker 创建RocketMq容器

**1**** 、拉取 ****rocketmq-4.3.2**  **的镜像**

docker pull rocketmqinc/rocketmq:4.3.2

![](RackMultipart20230818-1-nx22ha_html_25af85cdff2c8f6e.png)

**2**** 、在宿主机创建目录**

mkdir -p /data/namesrv/logs

mkdir -p /data/namesrv/store

mkdir -p /data/broker/logs

mkdir -p /data/broker/store

**3**** 、使用镜像启动 **** NameServer **** 容器**

docker run -d -p 9876:9876 -v /data/namesrv/logs:/root/logs -v /data/namesrv/store:/root/store-v /data/broker/broker.conf:/opt/rocketmq-4.3.2/conf/broker.conf --name rmqnamesrv rocketmqinc/rocketmq:4.3.2 sh mqnamesrv

**4**** 、使用镜像启动 ****broker**  **容器（说明：** -Xms512m 等内存值可根据机器实际内存值进行调整 **）**

docker run -d -p 10911:10911 -p 10909:10909 -v /data/broker/logs:/root/logs -v /data/broker/store:/root/store-v /data/broker/broker.conf:/opt/rocketmq-4.3.2/conf/broker.conf --name rmqbroker --link rmqnamesrv:namesrv -e "NAMESRV\_ADDR=namesrv:9876" -e "JAVA\_OPT=${JAVA\_OPT} -server -Xms512m -Xmx512m -Xmn256m -XX:PermSize=128m -XX:MaxPermSize=128m" rocketmqinc/rocketmq:4.3.2 sh mqbroker -c /opt/rocketmq-4.3.2/conf/broker.conf

启动之后进入 rmqnamesrv容器创建主题

sh bin/mqadmin updateTopic -n localhost:9876 -c DefaultCluster -t pushMessage

sh bin/mqadmin updateTopic -n localhost:9876 -c DefaultCluster -t xmppMessage

sh bin/mqadmin updateTopic -n localhost:9876 -c DefaultCluster -t userStatusMessage

sh bin/mqadmin updateTopic -n localhost:9876 -c DefaultCluster -t HWPushMessage

sh bin/mqadmin updateTopic -n localhost:9876 -c DefaultCluster -t fullPushMessage

sh bin/mqadmin updateTopic -n localhost:9876 -c DefaultCluster -t keywordMessage

1.
## Docker 创建third-push容器

1. **在**** third ****-push**** 的部署文件 ****third**** -push ****中创建**  **third**** -push\_dockerfile ****文件 ，写入如下内容**

FROM java:8

VOLUME /opt/third-push/logs

COPY application.properties /opt/third-push/application.properties

COPY \*.p12 /opt/third-push/

COPY sixth-hawk-164509-firebase-adminsdk-342gn-465351f0ef.json /opt/third-push/sixth-hawk-164509-firebase-adminsdk-342gn-465351f0ef.json

ADD third-push-1.0.war /opt/third-push/third-push-1.0.war

RUN bash -c 'touch /opt/third-push/third-push-1.0.war'

ENTRYPOINT ["java","-jar","/opt/third-push/third-push-1.0.war","--spring.config.location=/opt/third-push/application.properties"]

**说明：** 这里的application.properties 从 conf\_file/third-push目录里拷贝

.p12 文件为ios 推送证书文件

sixth-hawk-164509-firebase-adminsdk-342gn-465351f0ef.json 为Google 推送需要的文件

third-push-1.0.war 为 third-push 服务部署包

**2**** 、通过 ****dockerfile**  **文件构建镜像**

docker build -t third-push -f third-push\_dockerfile ./

**3**** 、通过镜像启动容器**

docker run -d -e "MONGODB\_ADDR=192.168.0.151:28018" -e "NAMESRV\_ADDR=192.168.0.155:9876" -e "XMPP\_HOST=192.168.0.155" -e "XMPP\_SERVERNAME=im.shiku.co" -e "REDIS\_ADDR=redis://192.168.0.155:6379" --name third-push-server third-push

## 8.Docker 创建message-push 容器

**1**** 、在 ****message-push**** 的部署文件 ****message-push**** 中创建 **** message-push\_dockerfile ****文件 ，写入如下内容**

FROM java:8

VOLUME /opt/message-push/logs

COPY application.properties /opt/message-push/application.properties

ADD xmpp-push-0.0.1-SNAPSHOT.war /opt/message-push/xmpp-push-0.0.1-SNAPSHOT.war

RUN bash -c 'touch /opt/message-push/xmpp-push-0.0.1-SNAPSHOT.war'

ENTRYPOINT ["java","-jar","/opt/message-push/xmpp-push-0.0.1-SNAPSHOT.war","--spring.config.location=/opt/message-push/application.properties"]

**说明：** 这里的application.properties 从 conf\_file/message-push目录里拷贝

xmpp-push-0.0.1-SNAPSHOT.war 为 message-push 服务的部署包

**2**** 、通过 ****dockerfile**  **文件构建镜像**

docker build -t message-push -f message-push\_dockerfile ./

**3**** 、通过镜像启动容器**

docker run -d -e "MONGODB\_ADDR=192.168.0.151:28018" -e "NAMESRV\_ADDR=192.168.0.151:9876" -e "XMPP\_HOST=192.168.0.151" -e "XMPP\_SERVERNAME=im.shiku.co" -e "REDIS\_ADDR=redis://192.168.0.151:6379" --name message-push-server message-push

## 9.Docker 创建Upload容器

**1**** 、在 ****upload**** 的部署文件 ****upload**** 中创建 **** upload\_dockerfile ****文件 ，写入如下内容**

FROM java:8

VOLUME /opt/upload/logs

COPY application.properties /opt/upload/application.properties

ADD upload-2.0.war /opt/upload/upload-2.0.war

RUN bash -c 'touch /opt/upload/upload-2.0.war'

RUN mkdir -p /data/www/resources

ENTRYPOINT ["java","-jar","/opt/upload/upload-2.0.war","--spring.config.location=/opt/upload/application.properties"]

**说明：** 这里的application.properties 从 conf\_file/upload目录里拷贝

upload-2.0.war 为 upload 服务的部署包

**2**** 、通过 ****dockerfile**  **文件构建镜像**

docker build -t upload -f upload\_dockerfile ./

**3**** 、在宿主机创建文件存储目录，挂载到容器****(****可将下面命令复制后一次执行****)**

mkdir -p /data/www/resources

cd /data/www/resources

mkdir audio

mkdir avatar

mkdir avatar/o

mkdir avatar/t

mkdir avatar\_r

mkdir avatar\_r/o

mkdir avatar\_r/t

mkdir gift

mkdir image

mkdir image/o

mkdir image/t

mkdir other

mkdir preview

mkdir temp

mkdir u

mkdir video

**4**** 、通过镜像启动容器**

docker run -d -p 8088:8088 -v /data/www/resources:/data/www/resources -e "FILE\_URL=http://file.shiku.co" -e "MONGODB\_URL=mongodb://192.168.0.151:28018" --name upload-server upload

1.
## Docker 创建Nginx容器

**说明：这里**** Nginx **** 主要提供文件访问服务，需要和 **** Upload **** 放在同一宿主机，以便能读取到上传的文件**

**1**** 、拉取官方镜像**

docker pull nginx

1. **在宿主机创建目录，编辑配置文件**

mkdir -p /data/nginx/logs

mkdir -p /data/nginx/conf

cd /data/nginx/conf

vim nginx.conf

写入如下内容：

user root;

worker\_processes 1;

pid /run/nginx.pid;

events {

worker\_connections 1024;

}

http {

include mime.types;

default\_type application/octet-stream;

#log\_format main '$remote\_addr - $remote\_user [$time\_local] "$request" '

# '$status $body\_bytes\_sent "$http\_referer" '

# '"$http\_user\_agent" "$http\_x\_forwarded\_for"';

access\_log /var/log/nginx/access.log;

error\_log /var/log/nginx/error.log;

sendfile on;

#tcp\_nopush on;

#keepalive\_timeout 0;

keepalive\_timeout 65;

#gzip on;

#文件访问

server{

listen 8089;

charset utf-8;

location / {

if ($http\_referer ~\* ".php") {

return 403;

}

root /www/resources;

expires 5d;

}

}

}

**3**** 、通过镜像启动容器**

docker run -p 8089:8089 --name nginx -v /data/www/resources:/www/resources -v /data/nginx/conf/nginx.conf:/etc/nginx/nginx.conf -v /data/nginx/logs:/var/log/nginx  -d nginx

# 三、配置第三方短信服务

说明：项目目前集成了阿里云短信和天天国际短信(二选一)

阿里云短信： 在阿里云后台申请开通短信业务并创建好签名和模板,审核通过后即可配置测试

天天国际短信：注册账号后需要通过QQ联系客服备案短信模板，并开通国内短信

![](RackMultipart20230818-1-nx22ha_html_2b1adfabf80584d8.png)

![](RackMultipart20230818-1-nx22ha_html_c2b21940912ec2e3.png)

![](RackMultipart20230818-1-nx22ha_html_53a8c698799e7a43.png)

# 四、配置微信充值与提现

## 1.配置微信充值

注意：首先确保拥有 **微信开放平台** 的账号，没有的话请注册一个

微信开放平台网址：[https://open.weixin.qq.com/](https://open.weixin.qq.com/)

1 ) 登录微信开放平台，点击管理中心，然后点击创建移动应用按照提示填写应用资料，

提交审核。

![](RackMultipart20230818-1-nx22ha_html_5297ab81afec41fb.png)

![](RackMultipart20230818-1-nx22ha_html_e181f3c9f645b9fb.png)

![](RackMultipart20230818-1-nx22ha_html_fff162f9da0b7140.png)

## 2.配置微信提现

1. 填写完成后，提交微信审核，应用审核通过后只有登录、分享等基础接口的权限，支付权限需要申请开通

![](RackMultipart20230818-1-nx22ha_html_435c50181125ab89.png)

1. 点击申请开通，在打开的页面填写商户信息，提交微信审核

![](RackMultipart20230818-1-nx22ha_html_62e8207f099ca2c.png)

1. 当微信审核通过后，该应用就具备了支付权限

![](RackMultipart20230818-1-nx22ha_html_9a5664748ce02b3.png)

1. **进行配置**

在 spring-boot-imapi 项目下打开 application.properties 配置文件，找到

微信支付相关配置,然后参照如下修改配置

![](RackMultipart20230818-1-nx22ha_html_fff162f9da0b7140.png) ![](RackMultipart20230818-1-nx22ha_html_dc913ed9a739e508.png)

wxConfig.appid ： 应用的 AppId

wxConfig.secret ：应用的AppSecret

wxConfig.mchid ： 微信商户号

wxConfig.apiKey ： API密钥, 微信商户后台设置

wxConfig.callBackUrl ：支付成功后的回调接口url

wxConfig.pkPath ：微信商户平台下发的证书路径

注：微信商户平台网址：https://pay.weixin.qq.com/index.php/core/home/login

说明： **微信提现** 权限需要在微信商户平台获取(企业付款到零钱)，目前申请条件为 1、已获得微信支付权限达到三个月 2. 有连续一个月的流水

当获取提现权限后，从微信商户平台下载证书，配置上即可

## 3.配置支付宝相关

需申请开通 APP支付 (充值需要用到), 单笔转账 (支付宝提现用到)

说明： **单笔转账** 权限需要在支付宝开放平台获取，目前申请条件为 : 仅支持注册满90天,且已实名认证的企业支付宝账户签约;暂时不支持个体工商户及个人支付宝账户。

需要修改支付宝应用的appid ,app私钥 ,支付宝公钥 ,和pid,回调地址(支付宝后台也要设置该回调地址)

![](RackMultipart20230818-1-nx22ha_html_4ed79551b2aff3bf.png)

1.
# 推送、地图与Https 域名证书相关申请

## 1.小米推送

[https://dev.mi.com/console/appservice/push.html](https://dev.mi.com/console/appservice/push.html)

登陆 \> 消息推送

![](RackMultipart20230818-1-nx22ha_html_431c7f15fb6ff967.png)

创建应用

![](RackMultipart20230818-1-nx22ha_html_ddc4ea47d27a5ab5.png)

![](RackMultipart20230818-1-nx22ha_html_c637827e35ff75a6.png)

![](RackMultipart20230818-1-nx22ha_html_a7c0ff3ea458fdcc.png)

![](RackMultipart20230818-1-nx22ha_html_3158186c67f483a0.png)

## 2.华为推送

https://developer.huawei.com/consumer/cn/

![](RackMultipart20230818-1-nx22ha_html_ff925558b957a34c.png)

![](RackMultipart20230818-1-nx22ha_html_75109f1a51bae41f.png)

如没有应用需新建

![](RackMultipart20230818-1-nx22ha_html_9f80839e6a30afbf.png)

创建应用 手动添加包名

![](RackMultipart20230818-1-nx22ha_html_294ac28a926808e9.png)

## 3.魅族推送

http://open.flyme.cn/

![](RackMultipart20230818-1-nx22ha_html_67b11173ee905861.png)

![](RackMultipart20230818-1-nx22ha_html_56d9522aac0c83bc.png)

![](RackMultipart20230818-1-nx22ha_html_c20500ac86583067.png)

![](RackMultipart20230818-1-nx22ha_html_a40016e95968a13e.png)

![](RackMultipart20230818-1-nx22ha_html_d0580dd48d22d003.png)

![](RackMultipart20230818-1-nx22ha_html_b635b10de72586f6.png)

![](RackMultipart20230818-1-nx22ha_html_7ec08b25a0ac9ba5.png)

## 4.vivo推送

vivo 推送比较繁琐需要的资料比较多,需先创建应用提交 通过审核后才能开通. 可后续在申请

https://dev.vivo.com.cn/home

![](RackMultipart20230818-1-nx22ha_html_fc3a7babe45b64e.png)

![](RackMultipart20230818-1-nx22ha_html_b1c2d12ce23950db.png)

![](RackMultipart20230818-1-nx22ha_html_4dceca1e416ed80a.png)

没有应用需新建应用

![](RackMultipart20230818-1-nx22ha_html_28beada7f95202dd.png)

![](RackMultipart20230818-1-nx22ha_html_28ae764e0897c5f0.png)

创建应用提交审核

![](RackMultipart20230818-1-nx22ha_html_8f3372b533c5e785.png)

## 5.oppo推送

注:oppo 推送官方限制必须在其应用商店上线后才能收到推送

https://push.oppo.com/

![](RackMultipart20230818-1-nx22ha_html_51ec85a9f03e30e7.png)

![](RackMultipart20230818-1-nx22ha_html_7f6fd669548ee0df.png)

![](RackMultipart20230818-1-nx22ha_html_ce39351e04a93263.png)

![](RackMultipart20230818-1-nx22ha_html_d83d912eb6e839ab.png)

![](RackMultipart20230818-1-nx22ha_html_d5370e541ce0767f.png)

![](RackMultipart20230818-1-nx22ha_html_9c22d28e97713a5c.png)

![](RackMultipart20230818-1-nx22ha_html_83a849c89acc733.png)

![](RackMultipart20230818-1-nx22ha_html_591364a45806f9e7.png)

## 6.百度地图

http://lbsyun.baidu.com/

![](RackMultipart20230818-1-nx22ha_html_418419821b3866b1.png)

![](RackMultipart20230818-1-nx22ha_html_4ad57f33e4612a72.png)

![](RackMultipart20230818-1-nx22ha_html_a2307642c4b14039.png)

![](RackMultipart20230818-1-nx22ha_html_447921497d6c1062.png)

注: iosiOS SDK安全码组成：Bundle Identifier即包名

## 7.谷歌推送

[https://sixth-hawk-164509.firebaseio.com](https://sixth-hawk-164509.firebaseio.com/)

登陆谷歌账号后访问

![](RackMultipart20230818-1-nx22ha_html_b77c1db59b0dd9b4.png)https://console.firebase.google.com/

![](RackMultipart20230818-1-nx22ha_html_9deb84b3858bf9cf.png)

![](RackMultipart20230818-1-nx22ha_html_80368e770dc3ae64.png)

![](RackMultipart20230818-1-nx22ha_html_b93f51e3aea43b74.png)

创建应用后完善应用信息填写包名和应用名称

![](RackMultipart20230818-1-nx22ha_html_70b775e72268b900.png)

![](RackMultipart20230818-1-nx22ha_html_8ca622dbe49c665f.png)

下载该文件提供给我们

## 8.谷歌地图

[https://cloud.google.com/maps-platform/](https://cloud.google.com/maps-platform/)

登陆谷歌账号后选择

![](RackMultipart20230818-1-nx22ha_html_660583fa384ce0d3.png)

![](RackMultipart20230818-1-nx22ha_html_47d59522adf60d4d.png)

选择项目

启用后得到配置

![](RackMultipart20230818-1-nx22ha_html_a1157eadfd28ab4f.png)

## 9.Https 域名证书

![](RackMultipart20230818-1-nx22ha_html_37e22ec25697a035.png)

![](RackMultipart20230818-1-nx22ha_html_7d0f09f161aec69f.png)

![](RackMultipart20230818-1-nx22ha_html_475a69082f3beb33.png)

![](RackMultipart20230818-1-nx22ha_html_bb1c81c0fc471334.png)

![](RackMultipart20230818-1-nx22ha_html_80c1a64ccd7d5cf4.png)

完善信息. 域名如果是在阿里云购买的选自动dns验证即可

![](RackMultipart20230818-1-nx22ha_html_1570763573136537.png)

验证提交审核

1.
# 服务器管理、维护

**如何连接上服务器以**** xshell ****为示例**

![](RackMultipart20230818-1-nx22ha_html_e6eb3521d407385e.png)

![](RackMultipart20230818-1-nx22ha_html_2c340a4d1f2d2f0a.png)

![](RackMultipart20230818-1-nx22ha_html_c1ea23ebcccf1529.png)

然后确定并点击连接

![](RackMultipart20230818-1-nx22ha_html_d451ab09b650368f.png)

**相关问题排查处理**

1. **请求异常**** , ****请稍后重试**

当所有用户出现这个提示可能是http接口服务(spring-boot-imapi)出问题了

如果特别紧急需尽快处理可尝试重启该服务

切换目录

cd /opt/spring-boot-imapi/

停止

sh stop

查看进程是否还存在

ps -ef |grep imapi

![](RackMultipart20230818-1-nx22ha_html_cca5db1711a1060f.png)

进程不存在如上

即执行

sh start

启动

![](RackMultipart20230818-1-nx22ha_html_1b958a5f7d352814.png)

如果进程还存在 执行sh stop 停止不了可使用

Kill -9 进程id

强制停止

然后在执行

sh start

启动该服务

如果重启服务后还是请求异常可以先检查下服务器的磁盘和内存使用情况

内存使用情况查看

free -h

![](RackMultipart20230818-1-nx22ha_html_e2b4e5650ac18231.png)

如果剩余内存不足了,可以清理下缓存. 或适当的调整服务器内存大小

清理缓存

echo 1 \> /proc/sys/vm/drop\_caches

echo 2 \> /proc/sys/vm/drop\_caches

echo 3 \> /proc/sys/vm/drop\_caches

free -h

查看磁盘使用情况

df -h

![](RackMultipart20230818-1-nx22ha_html_8488035b08f45dc.png)

磁盘空间使用率达到了90%以上就会有问题了. 可以看下是调整下磁盘空间大小还是删除些东西

最后还是异常可观察下日志是否有错误日志

cd /opt/spring-boot-imapi/

tail -f logs/error.log

或联系我们

1. **消息发不出去收不到**  **,**  **一直连接中**

当所有用户出现这情况,可能是通讯服务出问题了

同上,如要尽快解决可先立马尝试重启该服务

**酷信版本**

cd /opt/IMServer/

停止

sh stop

查看进程是否还存在

ps -ef |grep IMServer

![](RackMultipart20230818-1-nx22ha_html_39948c5e74554192.png)

进程已经不存在已停止

即执行

sh start

启动

如果进程还存在 执行sh stop 停止不了可使用

![](RackMultipart20230818-1-nx22ha_html_6b458108a1579ade.png)Kill -9 进程id

强制停止

然后在执行

sh start

启动该服务

如果重启服务后还是请求异常可以先检查下服务器的磁盘和内存使用情况

内存使用情况查看

free -h

![](RackMultipart20230818-1-nx22ha_html_e2b4e5650ac18231.png)

如果剩余内存不足了,可以清理下缓存. 或适当的调整服务器内存大小

清理缓存

echo 1 \> /proc/sys/vm/drop\_caches

echo 2 \> /proc/sys/vm/drop\_caches

echo 3 \> /proc/sys/vm/drop\_caches

free -h

查看磁盘使用情况

df -h

![](RackMultipart20230818-1-nx22ha_html_8488035b08f45dc.png)

磁盘空间使用率达到了90%以上就会有问题了. 可以看下是调整下磁盘空间大小还是删除些东西

最后如果实在还是有问题请联系我们

1. **文件上传异常**

先检查下upload 进程是否存在

![](RackMultipart20230818-1-nx22ha_html_4750242e51969437.png)

上图所示upload进程已不在

执行

sh start

启动

之后在测试下文件上传

其他排查方法可参考 上述 1 . 2. 相关步骤操作

1. **群控制消息不推送**** , **** 导致禁言失效 或收不到邀请进群通知**

首先检查下进程是否存在

![](RackMultipart20230818-1-nx22ha_html_97d09fbf4fb08530.png)

注:如果存在多个message-push 进程也会有问题,需使用kill -9 进程id 强制停止 在重新启动

如果进程存在但还是有问题 ,就操作下禁言或者发起进群邀请并观察下message-push 如果未打印任何有日志,那就需要检查下rocketmq ,(或者先检查下imapi 日志是否有异常,消息是否有正常放入队列

![](RackMultipart20230818-1-nx22ha_html_e664c9e024b214d2.png)

message-push 日志查看

cd /opt/message-push/

tail -f logs/log.log

Rocketmq 检查

查看监听的端口

netstat -nltp

![](RackMultipart20230818-1-nx22ha_html_7033ec86737da497.png)

mq broker 正常时 10909 10911 10912 正常监听

mq namesrv 正常 9876 正常监听

如果 有 namesrv或broker 未启动可参考 [3.roketmq 启动](#_3.roketmq%20%E5%90%AF%E5%8A%A8) 启动相关服务 ,之后在测试下

如果Rocketmq已经启动且端口都有监听但还是有问题可重启下mq 看下是否能正常重启

mq启动停止参考 [3.roketmq 启动](#_3.roketmq%20%E5%90%AF%E5%8A%A8) 如果正常重启未有如何异常 可在测试下

如果broker 启动异常 先检查下 磁盘空间是否充足 不超过 90% 为正常

如果磁盘空间充足 但broker还是启动不了

可 清理下 /root/store/\* 下的文件 ,先将roketmq 停止在清理

之后在重新启动 , 和重新注册推送消息、用户状态话题

**Linux**** 常用命令大全**

相关资料百度很多

https://www.cnblogs.com/testlearn/p/11211463.html

命令详细使用查询

[https://man.linuxde.net/](https://man.linuxde.net/)

## 1.修改调整服务器最大连接数

使用以下命令查看当前最大连接数：（默认为1024，需要改大）

[root@shiku ~]# ulimit -n

1024

修改以下配置文件：

编辑 /etc/security/limits.conf

[root@shiku~]# vim /etc/security/limits.conf

root soft nofile 204800

root hard nofile 204800

\* soft nofile 204800

\* hard nofile 204800

在配置文件中添加以上内容

编辑 /etc/pam.d/login

[root@shiku~]# vim /etc/pam.d/login

session required pam\_limits.so

在配置文件中添加以上内容

将以上保存好，然后重启服务器，再使用ulimit -n

[root@shiku~]# ulimit -n

204800

## 2.查看监听的端口

当某个服务出现不能正常访问，使用如下命令会查看对应的端口是否处于监听状态

#[root@shiku~]#netstat -lntp

![](RackMultipart20230818-1-nx22ha_html_f65eca444ec85d2.png)

各个服务对应端口说明：

Spring-boot-imapi 数据接口服务 默认使用端口: 8092

IMServer 通讯服务 客户端使用5666，Web版使用5260端口

upload 文件上传服务 默认使用 8088 端口

mongodb 数据库 默认使用 28018 端口

Redis 缓存服务 默认使用6379 端口

Nginx 主要用于文件访问时的目录映射 使用8089端口

## 3.设置防火墙

**对外暴露尽量少的端口**** --- ****我们建议使用域名配置**  **im**** 的相关服务，不推荐使用 ****ip**  **，使用域名配置的话就只用对外暴露很少的端口。**

  1. Iptables

#开放80端口(HTTP)

[root@shiku~]# iptables -A INPUT -p tcp --dport 80 -j ACCEPT

#开放443端口(HTTPS)

[root@shiku~]# iptables -A INPUT -p tcp --dport 443 -j ACCEPT

3.2 firewall

Centos 7.0 自带的防火墙 为 firewall

安装：yum install firewalld

**firewalld**** 的基本使用**

启动：[root@shiku~]# systemctl start firewalld

查看状态：[root@shiku~]# systemctl status firewalld

禁用，禁止开机启动：[root@shiku~]# systemctl disable firewalld

停止运行：[root@shiku~]# systemctl stop firewalld

**firewall**** 开启和关闭端口**

以下都是指在public的zone下的操作，不同的Zone只要改变Zone后面的值就可以

添加：

[root@shiku~]#firewall-cmd --zone=public --add-port=80/tcp --permanent

注：（--permanent永久生效，没有此参数重启后失效）

重新载入：

[root@shiku~]#firewall-cmd --reload

查看：

[root@shiku~]#firewall-cmd --zone=public --query-port=80/tcp

删除：

[root@shiku~]#firewall-cmd --zone=public --remove-port=80/tcp --permanent

**firewall**  **端口绑定**** ip**

用于将某个端口给特定的ip访问，如 mongodb 的数据库端口

指定IP与端口

firewall-cmd --permanent --add-rich-rule="rule family="ipv4" source address="192.168.142.166" port protocol="tcp" port="5432" accept"

重新载入，使配置生效

[root@shiku~]#firewall-cmd --reload

查看配置结果

[root@shiku~]#firewall-cmd --list-all

## 4.查看日志

使用 tail -f 命令可以打印实时日志

如现在需要查看 spring-boot-imapi 的日志

首先进入spring-boot-imapi 服务的目录

[root@shiku~]# cd /opt/spring-boot-imapi

[root@shiku~]# tail -f log.log

注：如在查看日志后，需要回到命令行 按 Ctrl + C

## 5.服务的启动与关闭

Im 相关服务的目录下都会有一个 start 文件和一个 stop 文件

当需要停止这个服务时，在服务的目录下 执行 sh stop命令即可，

同理 启动则在 对应目录下执行 sh start 命令

如： 现在需要停止 spring-boot-imapi 服务

[root@shiku~]# cd /opt/spring-boot-imapi

[root@shiku~]# sh stop

#启动

[root@shiku~]# sh start

## 6.通过nginx 做端口转发

注： **Nginx**  **需要**** 1.9 **** 以上版本**

nginx在1.9版本之后可以充当端口转发的作用，即：访问该服务器的指定端口，nginx就可以充当端口转发的作用将流量导向另一个服务器，同时获取目标服务器的返回数据并返回给请求者。nginx的TCP代理功能跟nginx的反向代理不同的是：请求该端口的所有流量都会转发到目标服务器，而在反向代理中可以细化哪些请求分发给哪些服务器；另一个不同的是，nginx做TCP代理并不仅仅局限于WEB的URL请求，还可以转发如memcached、MySQL等点到点的请求

./configure --prefix=/opt/nginx1.9.11 --add-module=/opt/ngx\_cache\_purge-2.3

--with-stream

--add-module=/opt/ngx\_cache\_purge-2.3 ： 这里是添加 ngx\_cache\_purge-2.3 用于清理缓存可根据需要选择是否使用

--with-stream ： with-stream 是用于tigse端口转发、集群时所需的

在 /opt/nginx1.9.11/conf/nginx.conf 配置文件中添加如下配置

**注意：**  **stream {...}**  **要和**  **http{...}**  **同级**

stream {

upstream xmpp{

hash $remote\_addr consistent;

server 47.91.255.114:5222;

}

server {

listen 5222;

proxy\_connect\_timeout 5s;

proxy\_timeout 5s;

proxy\_pass xmpp;

}

}

如下图所示：

![](RackMultipart20230818-1-nx22ha_html_5577deb7d463bfc1.png)

## 7.通过(iptables /fireWall)做端口转发

Centos 6.X

1) 开启服务器的ip 转发功能，默认是关闭的。

临时修改：修改过后就马上生效，但如果系统重启后则又恢复为默认值0。

[root@shiku ~]# echo 1 \>/proc/sys/net/ipv4/ip\_forward

永久修改：

[root@shiku ~]# vim /etc/sysctl.conf

#找到下面的值并将0改成1 ，默认值0是禁止ip转发，修改为1即开启ip转发功能。

net.ipv4.ip\_forward = 1

![](RackMultipart20230818-1-nx22ha_html_65213fa8a45c39bf.png)

[root@shiku ~]# sysctl –p（使之立即生效）

![](RackMultipart20230818-1-nx22ha_html_e67c7e21ba14c518.png)

1. 配置端口转发

说明：将 47.75.89.57 的8088 端口 转至 47.91.255.114 下的 5222 端口

[root@shiku ~]#iptables -t nat -A PREROUTING --dst 47.75.89.57 -p tcp --dport 8088 -j DNAT --to-destination 47.91.255.114:5222

[root@shiku ~]#iptables -t nat -A POSTROUTING --dst 47.91.255.114 -p tcp --dport 5222 -j SNAT --to-source 47.75.89.57

[root@shiku ~]# service iptables save 保存 iptablea 规则

[root@shiku ~]# vim /etc/sysconfig/iptables

如下图所示，保存后会在 iptables 中产生如下内容

![](RackMultipart20230818-1-nx22ha_html_9fcb67f8cc689d71.png)

[root@shiku ~]# service iptables restart 重启iptables 服务

注：在 /etc/sysconfig/iptables 配置中 找到以下配置注释掉，默认是开启的

![](RackMultipart20230818-1-nx22ha_html_b52614f612d81550.png)

## 8.windows 系统下的端口映射

通过PortMapping 程序进行端口转发，PortMapping 支持 DNF TCP UDP端口映射

![](RackMultipart20230818-1-nx22ha_html_a31057eb9740aacc.png)

## 如何连接上服务器以xshell为示例

![](RackMultipart20230818-1-nx22ha_html_e6eb3521d407385e.png)

![](RackMultipart20230818-1-nx22ha_html_2c340a4d1f2d2f0a.png)

![](RackMultipart20230818-1-nx22ha_html_c1ea23ebcccf1529.png)

然后确定并点击连接

![](RackMultipart20230818-1-nx22ha_html_d451ab09b650368f.png)

## 相关问题排查处理

1.
### 请求异常,请稍后重试

当所有用户出现这个提示可能是http接口服务(spring-boot-imapi)出问题了

如果特别紧急需尽快处理可尝试重启该服务

切换目录

cd /opt/spring-boot-imapi/

停止

sh stop

查看进程是否还存在

ps -ef |grep imapi

![](RackMultipart20230818-1-nx22ha_html_cca5db1711a1060f.png)

进程不存在如上

即执行

sh start

启动

![](RackMultipart20230818-1-nx22ha_html_1b958a5f7d352814.png)

如果进程还存在 执行sh stop 停止不了可使用

Kill -9 进程id

强制停止

然后在执行

sh start

启动该服务

如果重启服务后还是请求异常可以先检查下服务器的磁盘和内存使用情况

内存使用情况查看

free -h

![](RackMultipart20230818-1-nx22ha_html_e2b4e5650ac18231.png)

如果剩余内存不足了,可以清理下缓存. 或适当的调整服务器内存大小

清理缓存

echo 1 \> /proc/sys/vm/drop\_caches

echo 2 \> /proc/sys/vm/drop\_caches

echo 3 \> /proc/sys/vm/drop\_caches

free -h

查看磁盘使用情况

df -h

![](RackMultipart20230818-1-nx22ha_html_8488035b08f45dc.png)

磁盘空间使用率达到了90%以上就会有问题了. 可以看下是调整下磁盘空间大小还是删除些东西

最后还是异常可观察下日志是否有错误日志

cd /opt/spring-boot-imapi/

tail -f logs/error.log

或联系我们

1.
### 消息发不出去收不到 , 一直连接中

当所有用户出现这情况,可能是通讯服务出问题了

同上,如要尽快解决可先立马尝试重启该服务

**酷信版本**

cd /opt/IMServer/

停止

sh stop

查看进程是否还存在

ps -ef |grep IMServer

![](RackMultipart20230818-1-nx22ha_html_39948c5e74554192.png)

进程已经不存在已停止

即执行

sh start

启动

如果进程还存在 执行sh stop 停止不了可使用

![](RackMultipart20230818-1-nx22ha_html_6b458108a1579ade.png)Kill -9 进程id

强制停止

然后在执行

sh start

启动该服务

如果重启服务后还是请求异常可以先检查下服务器的磁盘和内存使用情况

内存使用情况查看

free -h

![](RackMultipart20230818-1-nx22ha_html_e2b4e5650ac18231.png)

如果剩余内存不足了,可以清理下缓存. 或适当的调整服务器内存大小

清理缓存

echo 1 \> /proc/sys/vm/drop\_caches

echo 2 \> /proc/sys/vm/drop\_caches

echo 3 \> /proc/sys/vm/drop\_caches

free -h

查看磁盘使用情况

df -h

![](RackMultipart20230818-1-nx22ha_html_8488035b08f45dc.png)

磁盘空间使用率达到了90%以上就会有问题了. 可以看下是调整下磁盘空间大小还是删除些东西

最后如果实在还是有问题请联系我们

1.
### 文件上传异常

先检查下upload 进程是否存在

![](RackMultipart20230818-1-nx22ha_html_4750242e51969437.png)

上图所示upload进程已不在

执行

sh start

启动

之后在测试下文件上传

其他排查方法可参考 上述 1 . 2. 相关步骤操作

1.
### 群控制消息不推送, 导致禁言失效 或收不到邀请进群通知

首先检查下进程是否存在

![](RackMultipart20230818-1-nx22ha_html_97d09fbf4fb08530.png)

注:如果存在多个message-push 进程也会有问题,需使用kill -9 进程id 强制停止 在重新启动

如果进程存在但还是有问题 ,就操作下禁言或者发起进群邀请并观察下message-push 如果未打印任何有日志,那就需要检查下rocketmq ,(或者先检查下imapi 日志是否有异常,消息是否有正常放入队列

![](RackMultipart20230818-1-nx22ha_html_e664c9e024b214d2.png)

message-push 日志查看

cd /opt/message-push/

tail -f logs/log.log

Rocketmq 检查

查看监听的端口

netstat -nltp

![](RackMultipart20230818-1-nx22ha_html_7033ec86737da497.png)

mq broker 正常时 10909 10911 10912 正常监听

mq namesrv 正常 9876 正常监听

如果 有 namesrv或broker 未启动可参考 [3.roketmq 启动](#_3.roketmq%20%E5%90%AF%E5%8A%A8) 启动相关服务 ,之后在测试下

如果Rocketmq已经启动且端口都有监听但还是有问题可重启下mq 看下是否能正常重启

mq启动停止参考 [3.roketmq 启动](#_3.roketmq%20%E5%90%AF%E5%8A%A8) 如果正常重启未有如何异常 可在测试下

如果broker 启动异常 先检查下 磁盘空间是否充足 不超过 90% 为正常

如果磁盘空间充足 但broker还是启动不了

可 清理下 /root/store/\* 下的文件 ,(先将roketmq 停止在清理

之后在重新启动 , 和重新注册推送消息、用户状态话题

## Linux常用命令大全

相关资料百度很多

https://www.cnblogs.com/testlearn/p/11211463.html

命令详细使用查询

[https://man.linuxde.net/](https://man.linuxde.net/)

# 七、wss配置说明

下载tomcat 类型的ssl 转换为jks 类型 .   在IMServer添加配置即可

![](RackMultipart20230818-1-nx22ha_html_a026198db1cdc6a4.png)

websocket.port=5260

websocket.ssl=true

ssl.keyStoreFile=/opt/IMServer/socket.jks

ssl.password=

 SSL证书pfx格式转为jks  参考  ![](RackMultipart20230818-1-nx22ha_html_1c8cd9327b84a73a.png)https://blog.csdn.net/weixin\_43886319/article/details/89852566

SSL证书pfx格式转为jks

首先，从官网下载pfx文件

这里以tomcat为例，解压后是如下两个文件（.pfx文件就是证书，.txt则是初始密码）

将.pfx文件放入jdk/bin目录下，例如：F:\Java\jdk1.8.0\_66\bin，打开电脑命令提示符应用，通过cd命令到H:\Java\jdk1.8.0\_66\bin目录下

执行命令keytool -importkeystore -srckeystore xxx.pfx -destkeystore xxx.jks -srcstoretype PKCS12 -deststoretype JKS将在bin目录下生成对应的xxx.jks文件，中间会有输密码，输入前面txt文件的密码即可

原文链接：https://blog.csdn.net/weixin\_43886319/article/details/89852566

# 八、数据库加密、定时备份

## 1. MongoDB加密说明：

**Mongodb**  **加密：给每个库配置用户名和密码**

**# cd /opt/mongodb-3.4.0/bin**

**# ./mongo -port 28018**

**//**** 设置 ****admin**** 的账号密码**

**\> use**  **admin**

**\> db.createUser({user: "root",pwd: "root",roles: ["****root****"]})**

**# vim mongo.conf** //打开mongodb配置文件配置

# 开启授权认证

security:

authorization: enabled

保存，然后重启mongoDb

打开 application.properties 配置文件，在下图所示的两个地方配置上mongoDb的用户名和密码

![](RackMultipart20230818-1-nx22ha_html_71102b552a2d3565.png)

![](RackMultipart20230818-1-nx22ha_html_9b21ccdd44124a97.png)

然后打开IMServer的配置文件imserver.properties 配置文件，修改所有的mongoDb 连接URL，添加上用户名和密码，如下所示

**注：第一个**** root ****是**** userName ****，第二个**** root ****是**** password**

![](RackMultipart20230818-1-nx22ha_html_93c7516ae57bb418.png)

1.
## Mongodb 数据备份：

具体参考:

[https://www.runoob.com/mongodb/mongodb-mongodump-mongorestore.html](https://www.runoob.com/mongodb/mongodb-mongodump-mongorestore.html)

## 3.Redis 加密说明：

# cd redis-3.0.3/ 进入redis目录

# vim redis.conf

找到 requirepass 所在行，去掉行前的注释，并将 "foobared" 修改为所需的密码，保存文件

![](RackMultipart20230818-1-nx22ha_html_c12686ca5a87525a.png)

1. 打开 application.properties 配置文件，找到redis的相关配置，

在下图红框位置配置上和第一步对应的密码。

![](RackMultipart20230818-1-nx22ha_html_7203f0cbcacbd696.png)

# 九、搭建服务端代码开发环境（以IntelliJ IDEA 2018为例）

### 前期准备

1. jdk配置指定File \> Project Structure

![](RackMultipart20230818-1-nx22ha_html_51406555e3e2fcf7.png)

1. Maven 配置指定 File \> Settings

![](RackMultipart20230818-1-nx22ha_html_194ad084296e4b0f.png)

3.Lombok 插件安装

![](RackMultipart20230818-1-nx22ha_html_ac710a78b4d5f7e0.png)

之后需要重启下 idea

![](RackMultipart20230818-1-nx22ha_html_e4c1adc1b75cbb4f.png)

1.
## 打开项目

![](RackMultipart20230818-1-nx22ha_html_ff97d0a7c705f225.png)

![](RackMultipart20230818-1-nx22ha_html_3dcc4719ec1f47d0.png)

导入指定为maven module

![](RackMultipart20230818-1-nx22ha_html_6457165188b16f24.png)

![](RackMultipart20230818-1-nx22ha_html_6c4bb3fa0b1f5006.png)

![](RackMultipart20230818-1-nx22ha_html_abd5365a52e3f906.png)

![](RackMultipart20230818-1-nx22ha_html_100e0178b54c714e.png)

后面一路next 最后 Finish Apply ok . 其他项目一样的操作

导入后此时的项目结构如下：

![](RackMultipart20230818-1-nx22ha_html_54483c0e4a1f69e7.png)

1.
## 导入下载不到的jar包解决pom报错

将下载不到的maven 依赖包拷贝到本地maven仓库对应的目录中

在源码文件目录中找到maven\_jars.zip 文件解压

![](RackMultipart20230818-1-nx22ha_html_33aff5907ef914f.png)

解压后如下图所示：

![](RackMultipart20230818-1-nx22ha_html_ebd8c0acfea1f8c8.png)

然后刷新下

![](RackMultipart20230818-1-nx22ha_html_cd47ff34b2df01a3.png)

1.
## 编译并运行项目

### 1.编译打包

首此编译打包先将 common-paremt 公共模块 项目 maven install

其次 maven install

im-comm-modules项目maven clean、maven install

需要注意要等到maven clean执行完成，控制台打印BUILD SUCCESS后在执行maven install

![](RackMultipart20230818-1-nx22ha_html_4a58803aaca3fded.png)

最后install mianshi-parent

![](RackMultipart20230818-1-nx22ha_html_ea2f29f38f620d85.png)

SUCCESS 即编译打包成功, 相关服务target目录下会生成部署文件

![](RackMultipart20230818-1-nx22ha_html_9b0b66541b2c1fd6.png)

### 2.运行

#### 1.mianshi-im-api

修改配置文件application.properties 关于配置文件修改的具体步骤请参看本文档的项目linux直接部署部分。

请参照下图标记位置，找到配置文件对应的配置项进行修改

![](RackMultipart20230818-1-nx22ha_html_fce6641459b1f43b.png)

运行项目，找到 mianshi-im-api 项目中的 Application 类，

![](RackMultipart20230818-1-nx22ha_html_64aaf8f7b5742126.png)

右键

![](RackMultipart20230818-1-nx22ha_html_c2257fbe91b775a9.png)

#### 2.IMServer

IMServer 通讯服务

酷信即时通讯服务端找到 IMServer-聊天服务器

![](RackMultipart20230818-1-nx22ha_html_3aecabdd125814e8.png)

参考

参照Linux安装步骤中的第6歩修改 imserver.properties

右键执行start.bat脚本，即可启动IMServer

![](RackMultipart20230818-1-nx22ha_html_b4fd643c0e7b3aa8.png)

![](RackMultipart20230818-1-nx22ha_html_47b620735ce1ece6.png)

出现上述内容 目录下的 log.log 也没有异常 即启动成功

#### 3.message-push

message-push 控制消息消费推送服务 关于配置文件修改的具体步骤请参看本文档的项目部署部分。

修改配置后运行

![](RackMultipart20230818-1-nx22ha_html_c3d2e4257c88e4b0.png)

右键

![](RackMultipart20230818-1-nx22ha_html_62f240280140e48c.png)

#### 4.third-push

third-push 离线推送服务

![](RackMultipart20230818-1-nx22ha_html_7b3a62e7298b1238.png)

右键

![](RackMultipart20230818-1-nx22ha_html_8f35421b00c2cc9f.png)

#### 5.upload 项目

Upload 项目是用来上传文件的，基本不需要改动，关于配置文件修改的具体步骤请参看本文档的项目部署部分。

![](RackMultipart20230818-1-nx22ha_html_167811fdf550a069.png)

![](RackMultipart20230818-1-nx22ha_html_d91b4fa42f79036b.png)

**深圳市视酷信息技术有限公司** www.shiku.co
