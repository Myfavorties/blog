# Redis可以做什么
1. 缓存

    合理的使用缓存不仅可以加快数据的访问速度，而且能够有效降低后端数据源
    的压力。
2. 排行榜系统

    Redis提供了列表和有序集合数据结构，合理地使用这些数据结构可以很方便地
    构建各种排行榜系统
3. 计数器应用

    Redis天然支持计数功能而且技术的性能也非常好
4. 社交网络

    赞/踩、粉丝、共同好友/喜好、推送、下拉刷新等是社交网站的必备功能，
    Redis提供的数据结构可以相对比较容易地实现这些功能。
5. 消息队列系统

    消息队列系统可以说是一个大型网站的必备基础组件，因为其具有业务解耦、
    非实时业务削峰等特性。Redis提供了发布订阅功能和阻塞队列的功能
# Redis不可以做什么
    在数据规模的角度看，数据可以分为大规模数据和小规模数据，Redis的数据是
    存放在内存中，如果数据量到达亿级以上，经济成本相当的高。
# 用好Redis的建议
1. 切勿当做黑盒试用，开发与运维同样重要

    实际运维和使用Redis的过程中，很多线上问题和故障都是由于完全把Redis当
    做黑盒造成的,如果不了解Redis的单线程模型，有些开发者会在有上千万个键
    的Redis上配上执行keys *操作，如果不了解持久化的相关原理，会在一个写操
    作量很大的Redis上配置自动保存RDB。而且在很多公司内只有专职的关系型数
    据库DBA，并没有NoSQL的相关运维人员，也就是说开发者很有可能会自己运
    维Redis，对于Redis的开发者来说既是好事又是坏事。站在好的方面看，开发
    人员可以通过运维Redis真正了解Redis的一些原理，不单纯停留在开发上。站
    在坏的方面看，Redis的开发人员不仅要支持开发，还要承担运维的责任，而且
    由于运维经验不足可能会造成线上故障。但是从实际经验来看，运维足够规模
    的Redis会对用好Redis更加有帮助
2. 阅读源码

    Redis是开源项目，作者对Redis代码的极致追求，Redis的代码量相对于许多
    NoSQL数据库来说非常小，意味着作为普通的开发和运维人员也是可以吃透
    Redis源码。通过阅读优秀的源码，不仅能够加深我们对于Redis的理解，而且
    还能提高自身的编码水平，甚至可以对Redis做定制化，也就是说可以修改
    Redis的源码来满足自身的需求。
# 正确安装并启动Redis
1. 安装Redis

    Redis能兼容绝大部分的POSIX系统，例如Linux、OS X、OpenBSDNetBSD和
    FreeBSD，其中比较典型的是Linux操作系统（例如CentOS、Redhat、
    Ubuntu、Debian、OS X等）。在Linux安装软件通常有两种方法，第一种是通
    过各个操作系统的软件管理软件进行安装，例如CentOS有yum管理工具，
    Ubuntu有apt。但是由于Redis的更新素对相对较快，而这些管理工具不一定能
    更新到最新版本，同事前面提到Redis的安装本身不是很复杂，所以一般推荐第
    二种方式：源码的方式进行安装，整个安装只需一下六步即可完成，以3.0.7版
    本为例：
    
    ```
        $ wget http://download.redis.io/releases/redis-3.0.7.tar.gz
        $ tar xzf redis-3.0.7.tar.gz
        $ ln -s redis-3.0.7 redis
        $ cd redis
        $ make 
        $ make install
    ```
    - 1） 下载Redis指定版本的源码压缩包到当前目录。
    - 2） 解压缩Redis源码压缩包。
    - 3） 建立一个redis目录的软连接，指向redis-3.0.7。
    - 4） 进入redis目录。
    - 5） 编辑（编译之前确保操作系统已经安装gcc）。
    - 6） 安装。

    这里有两点要注意：第一，第3不中简历一个redis目录的软连接，这样做是为
    了不把redis目录固定在指定版本上，有利于Redis未来版本升级，算是安装软
    件的一种好习惯。第二，第6步中的安装是将Redis的相关运行文件放到
    /usr/local/bin/下，这样就可以在任意目录下执行Redis的命令。

2. 在Windows中安装Redis
    Redis的官方并不支持微软的Windows操作系统，但是微软公司的开源技术组在
    GitHub上维护了一个Redis的分支：
    https://gihub.com/MSOpenTech/redis

3. 配置、启动、操作、关闭Redis

    可执行文件|作用
    -|-
    redis-server|启动Redis
    redis-cli|Redis命令行客户端
    redis-benchmark|Redis基准测试工具
    redis-check-aof|Redis AOF持久化文件检测和修复工具
    redis-check-dump|Redis RDB持久化文件检测和修复工具
    redis-sentinel|启动Redis Sentinel


