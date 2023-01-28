# Linux 前置设置
## 集群环境
```text
centos 7

c-node01 192.168.25.139
c-node02 192.168.25.149
c-node03 192.168.25.150
c-node04 192.168.25.151

```


## 静态IP设置
```shell
# 查看本机ip 
ifconfig # 如果没有使用yum安装 yum install net-tools.x86_64

# 查看虚拟网络编辑器网关设置
# 修改 /etc/sysconfig/network-scripts/ifcfg-ens* 文件
BOOTPROTO="static"  # dhcp 为动态
IPADDR="192.168.25.149"
GATEWAY="192.168.25.2"
NETMASK="255.255.255.0"
DNS1="114.114.114.114"

# 修改 /etc/resolv.conf 文件
# 114.114.114.114 为电信域名解析
# 8.8.8.8 为google
nameserver 114.114.114.114

# 重启网络服务
/etc/init.d/network restart

# 设置主机名称
echo -e "NETWORKING=yes\nHOSTNAME=c-node01" >> /etc/sysconfig/network

```

## 集群间免密
```shell
# 验证自己是否免密，被动生成 /root/.ssh 目录
ssh localhost

# 创建密钥
ssh-keygen -t dsa -P '' -f ~/.ssh/id_dsa
# -t 加密算法 rsa dsa
# -P 密码
# -f 密钥存放路径
# 想登录谁，就将密钥发送给谁，将公钥添加到 authorized_keys 文件中
cat ~/.ssh/id_dsa.pub >> ~/.ssh/authorized_keys
```
### SSR

## JVM 环境安装

[jdk1.8 rpm包](https://www.oracle.com/cn/java/technologies/javase/javase8-archive-downloads.html)
```shell
# rpm 方式安装
rpm -i jdk-8u181-linux-x64.rpm

# 有一些软件只认： /usr/java/default

# 设置JAVA_HOME
vim /etc/profile

export JAVA_HOME=/usr/java/default
export PATH=$PATH:$JAVA_HOME/bin

# 重新加载profile文件
# source /etc/profile
# 或者
. /etc/profile
```

## 统一时间设置

```shell
# 时间同步
yum install ntp -y

# 设置向阿里云服务器同步时间
vim /etc/ntp.conf
  server ntp1.aliyun.com

# 设置开机自启动
centos 6:
service ntpd start
checkconfig ntpd on
centos 7:
systemctl start ntpd
systemctl enable ntpd
```

## 常用工具安装