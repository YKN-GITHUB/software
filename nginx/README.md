# Install nginx

[nginx](http://nginx.org/)

## Install nginx for ubuntu

### 前置环境安装

```sh
apt-get install -y gcc libpcre3 libpcre3-dev zlib1g-dev openssl libssl-dev
```

> 在类unix系统中1024端口以下需要使用root用户才能使用



## Install nginx for linux

```sh
yum install -y gcc zlib zlib-devel pcre-devel openssl openssl-devel
```



## 编译 & 安装 nginx

```sh
./configure --prefix=PATH --with # 需要加载的模块
make
make install
```

