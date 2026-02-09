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

一些主流的数据库：
- SQL Sever: 微软的产品，.Net 程序员的最爱，中大型项目。
- Oracle: 甲骨文产品，适合大型项目，复杂的业务逻辑，并发一般来说不如MySQL。
- MySQL: 世界上最受欢迎的数据库，属于甲骨文，并发性好，不适合做复杂的业务。主要用在电商，SNS，论坛。对简单的SQL处理效果好。
- PostgreSQL: 加州大学伯克利分校计算机系开发的关系型数据库，不管是私用，商用，还是学术研究使用，可以免费使用，修改和分发。
- SQLite: 是一款轻型的数据库，是遵守ACID的关系型数据库管理系统，它包含在一个相对小的C库中。它的设计目标是嵌入式的，而且目前已经在很多嵌入式产品中使用了它，它占用资源非常的低，在嵌入式设备中，可能只需要几百K的内存就够了。
- H2: 是一个用Java开发的嵌入式数据库，它本身只是一个类库，可以直接嵌入到应用项目中。

**SQL语句的分类：**
- DDL: Data Definition Language 数据定义语言，用来维护存储数据的结构，比如 `create`, `drop`, `alter`, ...
- DML: Data Manipulation Language 数据操纵语言，用来对数据进行操作，比如 `insert`, `delete`, `update`, ...
  - DML中又单独分了一个 DQL, 数据查询语言，代表指令 `select`
- DCL: Data Control Language 数据控制语言，主要负责权限管理和事务，比如 `grant`, `revoke`, `commit`, ...

**MySQL的一些存储引擎：**

存储引擎其实就是底层如何把数据存储起来的方法，这个也很好理解。`show engines;` 就可以查看MySQL配置有的一些存储引擎，最常用的就是 InnoDB, 其次就是 MySAM，然后还有一些其他的，也不用去管太多。


## 操作

