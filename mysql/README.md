# Learn mysql one more time

Learn how to use mysql one more time!


版本：
![alt text](./assets/image.png)

因为这部分内容已经非常熟悉了，所以我这里只稍微补充一些内容，和一些进阶的内容。同样也是从操作开始。

## 前言

```bash
mysql -h 127.0.0.1 -P 3306 -u root -p
```

mysql是个网络服务，`-h` 表示连接哪一台主机上的 mysql, `-P` 表示端口号，`-u` 表示登陆哪个用户 `-p` 表示密码。

只是配置文件里配置之后，`mysql` 默认登陆本地的。

然后我自己用这条命令的时候登不进去，原因是这样的：

> 是 Ubuntu/Debian 默认把 MySQL 的 root 账号设成 auth_socket 认证 导致的。

> 发生了什么
> - 直接 mysql 能进去：因为你是 Linux 的 root 用户，MySQL 允许你通过 socket 方式 免密码登录 root@localhost。
> - 用 `-h 127.0.0.1 -u root -p` 进不去：一旦你指定 -h，客户端会走 TCP（即使是 127.0.0.1），这时候 auth_socket 不适用，于是报 ERROR 1698
> 所以：mysql（socket）能进，但 mysql -h 127.0.0.1（TCP）会拒绝 —— 这就是正常现象。


我这个mysql的配置文件都在这里：
- 主配置：`/etc/mysql/my.cnf`
- 服务配置：`/etc/mysql/mysql.conf.d/mysqld.cnf`
- 其他片段：`/etc/mysql/conf.d/`


然后就是 mysqld 和 mysql 的区别，前者是服务端后者是客户端。

