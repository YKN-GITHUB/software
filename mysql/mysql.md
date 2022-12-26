# Mysql 



## Install MySQL on Ububtu

```sh
sudo apt-get install -y mysql-server # 下载Mysql-Server程序

# MySQL 初始化操作 
## 为root用户设置密码 权限 ** 这种方式在mysql8.x版本中是语法错误的
# GEANT ALL PRIVILEGES ON *.* TO root@localhost IDENTIFIED BY "123"
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '333';
# 设置mysql白名单
# /etc/mysql/mysql.conf.d/mysqld.cnf
# 注释掉 bind相关配置
# Instead of skip-networking the default is now to listen only on
# localhost which is more compatible and is not less secure.
# bind-address          = 127.0.0.1
# mysqlx-bind-address   = 127.0.0.1
```

