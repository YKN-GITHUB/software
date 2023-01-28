# [zookeeper](https://www.apache.org/dyn/closer.lua/zookeeper/zookeeper-3.7.1/apache-zookeeper-3.7.1-bin.tar.gz) 

## install zookeeper cluster
[前置环境 JVM 集群免密 设置静态IP](https://github.com/YKN-GITHUB/software/blob/main/preposition/Linux%E5%89%8D%E7%BD%AE%E8%AE%BE%E7%BD%AE.md)
````shell

# 推荐大于2台机器的奇数机器数
# 下载地址 https://www.apache.org/dyn/closer.lua/zookeeper/zookeeper-3.7.1/apache-zookeeper-3.7.1-bin.tar.gz
# 解压缩
tar xf apache-zookeeper-3.7.1-bin.tar.gz
# 重命名
mv apache-zookeeper-3.7.1-bin.tar.gz zk
# 修改配置文件
cd /zk/conf
cp zoo_sample.cfg zoo.cfg

# 修改重点
# 数据持久化目录
dataDir=/tmp/zookeeper
# 集群过半，需要标清节点
# 需要向 dataDir 目录下 创建 myid文件进行标识
# server.nodeID=nodeIP:2888(leader启动2888，leader接收写请求的):3888(集群内部连接通讯投票选择leader)
server.1=node01:2888:3888
server.2=node02:2888:3888
server.3=node03:2888:3888
server.4=node04:2888:3888 

# 创建标识文件 myid
mkdir  /var/zookeeper
echo "1" >> /var/zookeeper/myid
# 修改 profile 文件
export ZOOKEEPER_HOME=/opt/zookeeper/zk
export PATH=$PATH:$JAVA_HOME/bin:$ZOOKEEPER_HOME/bin

# 重新加载 profile文件
. /etc/profile

# 前台启动 zk 集群
zkServer.sh [--config <conf-dir>] {start|start-foreground|stop|version|restart|status|print-cmd}
zkServer.sh start-foreground    # 前台启动

````