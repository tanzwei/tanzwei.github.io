### Redis

1. Redis简介：Redis是一种数据库。能够存储数据，管理数据的一种软件。是一个用C语言编写的、开源的、基于内存运行并支持持久化的、高性能的NoSQL数据库。

2. Redis的优势：
   - 运行在内存中，速度快。（Redis中的数据大部分时间都是存储在内存中的，适合存储频繁访问，数据量较小的数据）
   - 数据虽然在内存，但是提供了持久化的支持，即可以将内存中的数据异步写入到硬盘中，同时不影响继续提供服务。
   
3. Redis的特点：
   - 支持数据持久化。（可以将内存中的数据保存在磁盘中，重启的时候可以再次加载进行使用）
   - 支持多种数据结构。
   - 支持数据备份。（即 master-slave 模式的数据备份）
   
4. Redis数据结构：Redis是一种高级的key:value存储系统，其中value支持五种数据类型：
   - String -- 字符串
   - List -- 链表
   - Set -- 集合
   - Hash -- 哈希类型
   - Zset -- 有序集合
   
5. 启动redis服务：

   1. 前台启动：在任何目录下执行 --> redis-server（使用较少）
   2. 后台使用：redis-server &
   3. 启动redis服务时，指定配置文件：redis-server redis.conf &

6. 查看redis是否启动：ps -ef|grep redis

7. 关闭redis服务：

   1. 通过kill命令：（不推荐）

      ```
      ps -ef|grep redis 查看pid（第一行的第一个数字）
      kill -9 pid
      ```

   2. 通过redis-cli命令关闭：redis-cli shutdown

8. redis的客户端：用来连接redis服务，向redis服务端发送命令，并且显示redis服务处理结果。

   - redis-cli：是redis自带客户端，使用redis-cli就可以启动redis的客户端程序。

     ```
     redis-cli：默认链接127.0.0.1(本机)的端口号上的redis服务。
     redis-cli -p 端口号：连接127.0.0.1的指定端口上的redis服务。
     redis-cli -h ip地址 -p 端口：连接指定ip主机上的指定端口的redis服务。
     ```

   - 退出客户端：在客户端执行命令：exit 或 quit

9. redis的基本知识：

   - 测试redis服务的性能：redis-benchmark
   - 查看redis服务是否正常运行：ping  -->如果正常 --> PONG
   - 查看redis服务器的统计信息：
     - info  查看redis服务的所有统计信息
     - info 信息段  查看redis服务器的指定的统计信息
   - redis的数据库实例：作用类似于mysql的数据库实例，redis中的数据库实例只能由redis服务来创建和维护，开发人员不能修改和自行创建数据库实例;默认情况下，redis会 自动创建16个数据库实例，并且给这些数据库实例进行编号，从0开始，一直到15，使用时通过编号来使用数据库;可以通过配置文件，指定redis自动创建的数据库个数; redis的每一个 数据库实例本身占用的存储空间是很少的，所以也不造成存储空间的太多浪费。
     - 默认情况下，redis客户端连接的是编号为0的数据库实例，可以使用 select index(下标) 切换数据库实例.
   - 查看当前数据库实例中所有key的数量: dbsize
   - 查看当前数据库实例中所有的key：keys *
   - 清空数据库实例: flushdb
   - 清空所有的数据库实例: flushall
   - 查看redis中所有的配置信息: config get *
     查看redis中的指定的配置信息: config get parameter

10. redis安装步骤

   - Redis是基于C语言编写的，因此首先要安装gcc依赖：

      ```
      yum install -y gcc tcl
      ```

   - 将Redis安装包放到：`/usr/local/src` 目录

   - 解压：

      ```
      tar -zxvf redis文件名
      ```

   - 进入redis目录

   - 运行编译命令：

      ```
      make && make install
      ```

   - 默认安装路径是在：`/usr/local/bin` 目录下

   - 备份配置文件：

      ```
      cp redis.conf redis.conf.bac
      ```

   - 修改redis.conf文件中的一些配置：

      ```
      #允许访问的地址，默认是127.0.0.1，会导致只能在本地访问。修改为0.0.0.0则可以在任意ip访问，生产环境要设置0.0.0.0
      bind 0.0.0.0
      
      #守护进程，修改为yes后即可后台运行
      daemonize yes
      
      #密码，设置后访问redis必须要输入密码
      requir
      ```

      

11. redis中的操作命令:

    1. redis中有关key的操作命令:

       ```
       查看数据库中的key: keys pattern
       						-->*: 匹配0个或者多个字符
       						-->?: 匹配1个字符
       						-->[]:匹配[]里边的1个字符
       eg：
       	keys *：查看数据库中所有的key
       	keys k*：查看数据库中所有以k开头的key
       	keys h*o：查看数据库中所有以h开头，以o结尾的key
       	keys h?o：查看数据库中所有以h开头、以o结尾的、并且中间只有一个字符的key
       	keys h[abc]llo：查看数据库中所有以h开头以11o结尾，并且h后边只能取abc中的一个字符的key
       	
       判断key在数据库中是否存在：exists key；如果存在，则返回1，不存在返回0
       eg：
       	exists k1
       	exists k1 k2 k3
       	
       移动指定key到指定的数据库实例：move key index
       eg：
       	move temp 1
       	
       查看指定key的剩余生存时间：ttl key
       eg：
       	ttl k1（如果key没有设置生存时间，返回-1；如果key不存在，返回-2）
       	
       设置key的最大生存时间：expire key seconds
       eg：
       	expire k1 20
       	
       查看指定key的数据类型：type key
       eg：
       	type k1
       	
       重命名key：rename key newkey
       eg：
       	rename temp test
       	
       删除指定的key：del key -->返回的是实际删除的key的数量
       eg：
       	del k1 k2 k3
       ```

    2. redis中有关string类型数据的操作命令：

       ```
       将string类型的数据设置到redis中：set 键 值
       
       从redis中获取string类型的数据：get 键
       
       追加字符串：append key value
       			-->返回追加之后的字符串长度
       			-->如果key不存在，则新建一个value，并把追加的value值设置为value
       eg：
       	set phone 123
       	append phone 888
       	
       获取字符串长度数据的长度：strlen key
       
       将字符串数值进行加1运算: incr key
       						-->返回加1运算之后的数据
       						-->如果key不存在，首先设置一个key,值初始化为0，然后进行incr运算。
       						-->要求key所表示value必须是数值，否则，报错
       						
       将字符串数值进行减1运算: decr key
       						-->返回减1运算之后的数据
       						-->如果key不存在，首先设置一个key,值初始化为0，然后进行decr运算。
       						-->要求key所表示value必须是数值，否则，报错
       						
       将字符串数值进行加（减）offset运算: incrby（decrby） key offset
       						-->返回加（减）offset运算之后的数据
       						-->如果key不存在，首先设置一个key,值初始化为0，然后进行incrby（decrby）运算。
       						-->要求key所表示value必须是数值，否则，报错
       eg：
       	incrby zsage 10 --> zsage加10
       	
       闭区间获取字符串key中从startIndex到endIndex的字符组成的字符串：
       	getrange key startIndex endIndex --> 下标自左至右，从0开始。
       									 -->下标可以是负数，从右往左，从-1开始
       eg：
       	getrange zsname 2 5
       	
       用value覆盖下标为startIndex开始的字符串，能覆盖几个就覆盖几个：
       	setrange key startIndex value
       eg：
       	setrange zsname 5 xiaosan -->zhangxiaosan
       	setrange zsname 5 lao -->zhanglaoosan
       	
       设置字符串数据的同时，设置它的最大生命周期：setex key seconds value
       eg：
       	setex k1 20 v1
       	
       设置string类型的数据value到redis中，当key不存在时设置成功，否则，放弃设置：	
       	setnx key value
       eg：
       	setnx zsage 20
       	
       批量将string类型的数据设置到redis中：mset 键1 值1 键2 值2 .....
       eg：mset k1 v1 k2 v2 k3 v3 k4 v4 k5 v5
       
       批量从redis中获取string类型的数据：mget 键1 键2 键3
       mget k1 k2 k3 k4 k5 k6 zsname
       
       批量设置string类型的数据value到redis数据库中，当所有key都不存在时设置成功，否则(只要有一个已经存在)全部放弃设置：msetnx 键1 值1 键2 值2
       msetnx kk1 vv1 kk2 vv2 kk3 vv3 k1 v1
       ```

    3. redis中有关list类型数据的操作命令：

       - 单key-多有序value；一个key对应多个value;

       - 多个value之间有顺序，最左侧是表头，最右侧是表尾；每一个元素都有下标，表头元素的下标是0，依次往后排序，最后一个元素下标是列表长度-1;

       - 每一个元素的下标又可以用负数表示，负下标表示从表尾计算，最后一个元素下标用-1表示;

       - 元素在列表中的顺序或者下标由放入的顺序来决定。

         ```
         1、将一个或多个值依次插入到列表的表头(左侧)：lpush key value [value value ....]
         eg：lpush list01 1 2 3  结果：3 2 1
         	lpush list01 4 5    结果：5 4 3 2 1
         	
         2、获取指定列表中指定下标区间的元素：lrange key startIndex endIndex
         eg：lrange list01 1 3	结果：4 3 2
         	lrange list01 1 -2	 结果：4 3 2
         	lrange list01 0 -1   结果: 5 4 3 2 1
         	
         3、将一个或多个值依次插入到列表的表尾(右侧)：rpush key value [value value .....]
         eg：rpush list02 a b c	--> a b c
         	rpush list02 d e	 -->a b c d e
         	
         4、从指定列表中移除并返回表头元素：lpop key
         eg：lpop list02
         
         5、从指定列表中移除并返回表尾元素：rpop key
         
         6、获取列表中指定下标的元素：lindex key index
         
         7、获取指定列表的长度：llen key
         eg：llen list01
         
         8、根据count值移除指定列表中跟value相等的数据：lrem key count value
         													  |->count > 0：从列表的左侧移除count个跟value相等的数据;
         													  |->count < 0：从列表的右侧移除count个跟vlaue相等的数据;
         													  |->count = 0：从列表中移除所有跟value相等的数据。
         eg：lpush list03 a a b c a d e a b b  --> b b a e d a c b a a
         	lrem list03 2 a   --> b b e d c b a a
         	lrem list03 -1 a   --> b b e d c b a
         	lrem list03 0 a   --> b b e d c b
         	
         9、将指定列表中指定下标的元素设置为指定值：lset key index value
         eg：
         	lset list01 1 10
         ```

    4. redis中有关set类型数据的操作命令：

       - 单key - 多无序value

       - 一个key对应多个value

       - value之间没有顺序，并且不能重复

       - 通过业务数据直接操作集合

         ```
         1、将一个或多个元素添加到集合中：sadd key value [value value ...] 
         	*返回成功加入的元素
         	*不可存放重复元素
         --> sadd set01 a b c d 
         
         2、获取指定集合中所有的元素：smembers key
         --> smembers set01
         
         3、判断指定元素在指定集合中是否存在：sismember key member
         	*存在，返回1
         	*不存在，返回0
         --> sismember set01 f
         
         4、获取指定集合的长度：scard key
         --> scard set01
         
         5、移除指定集合中一个或多个元素：srem key member [member ....]
         	*不存在的元素会被忽略
         	*返回成功成功移除的个数
         --> srem set01 b d m
         
         6、随机获取指定集合中的一个元素：srandmember key [count]
         											   |-> count > 0：随机获取的多个元素不能重复
         											   |-> count < 0：随机获取的多个元素可能重复
         --> srandmember set01
         --> srandmember set01 2
         
         7、随机从指定集合中随机移除一个或多个元素：spop key [count]
         
         8、将指定集合中的指定元素移动到另一个集合：smove source dest member
         --> smove set01 set02 tzw
         
         9、获取第一个集合中有但是其它集合中都没有的元素组成新的集合：sdiff key key [...]
         --> sdiff set01 set02
         
         10、获取所有指定集合中都有的元素组成新的集合：sinter key key [...]
         --> sinter set01 set02
         
         11、获取所有指定集合中所有元素组成的大集合：sunion key key [...]
         --> sunion set01 set02
         ```

    5. redis中有关hash类型数据的操作命令：单key:field-value

       ```
       student:id-101
       		name-zhangsan
       		age-20
       ```

       ```
       1、将一个或多个field-value对设置到哈希表中：hset key field1 value1 [field2 value2]
       	*如果key field 已经存在，则value会把以前的值覆盖掉
       --> hset stu001 id 101
       --> hset stu001 name zhangsan age 20
       
       2、获取指定哈希表中指定field的值：gset key field
       --> hget stu001 id
       
       3、批量获取指定哈希表中的field的值：hmget key field1 [field 2 ...]
       --> hmget stu001 id name age
       
       4、获取指定哈希表中所有的field和value：hgetall key
       --> hgetall stu001
       
       5、从指定哈希表中删除一个或多个field：hdel key field1 [...]
       --> hdel stu001 id name 
       
       6、获取指定哈希表中所有的field个数：hlen key
       --> hlen stu001
       
       7、判断指定哈希表中是否存在某一个field：hexists key field
       --> hexists stu001 name
       
       8、获取指定哈希表中所有的field列表：hkeys key
       
       9、获取指定哈希表中所有的value列表：hvals key
       
       10、将一个field-value对设置到哈希表中，当key-field已经存在，则放弃设置：hsetnx key field value
       --> hsetnx stu001 age 30
       ```

    6. redis中有关zset类型数据的操作命令：

       - 有序集合，有下标

       - 本质上是集合，所有元素不能重复

       - 每一个元素都关联一个分数，redis会根据分数对元素进行自动排序(从小往大)

       - 分数可以重复

          ```
          （排序默认从小到大）
          1、将一个或多个member及score值加入有序集合：zadd key score member [score member ..]
          	*如果元素存在，则把分数覆盖
          --> zadd zset01  20 z1 30 z2 23 z3 40 z4
          	zadd zset01 60 z2 （将z2的分数换为60）
          	
          2、获取指定有序集合中指定下标区间的元素：zrange key startIndex endIndex [withscores]
          --> zrange zset01 0 -1 (显示分数)
          --> zrange zset01 0 -1 withscores (显示元素和分数)
          
          3、获取指定有序集合中指定分数区间(闭区间)的元素：zrangebyscore key min max [withscores]
          --> zrangebyscore zset01 60 100 withscores
          
          4、删除指定有序集合中一个或多个元素：zrem key member [member ...]
          --> zrem zset01 z3 z4
          
          5、获取指定有序集合中所有元素的个数：zcard key
          --> zcard zset01
          
          6、获取指定有序集合中分数在指定区间内的元素的个数：zcount key min max
          --> zcount zset01 20 50
          
          7、获取指定有序集合中指定元素的排名（下标从0开始，从小到大）：zrank key member
          --> zrank zset01 z3
          
          8、获取指定有序集合中指定元素的分数：zscore key member
          --> zscore zset01 z4
          
          9、获取指定有序集合中指定元素的排名（按照分数从大到小）：zrevrank key member
          --> zrevrank zset01 z4
          ```

12. redis的配置文件：在redis根目录下提供redis.conf配置文件：

    ```
    - 可以配置一些redis服务端运行时的一些参数；
    - 如果不使用配置文件，那么redis会按照默认的参数运行；
    - 如果使用配置文件，在启动redis服务时必须指定所使用的配置文件。
    ```

    - redis配置文件中关于网络的配置：

      ```
      1、port：指定redis服务所使用的端口，默认使用6379。
      
      2、bind：配置客户端连接redis服务时，所能使用的ip地址，默认可以使用redis服务所在主机上任何一个ip都可以；一般情况下，都会配置一个ip，而且通常是一个真实的。
      
      3、如果配置了port和bind,则客户端连接redis服务时，必须指定端口和ip:
      	redis-cli -h 192.168.11.128 -p 6380
      	redis-cli -h 192.168.11.128 -p 6380 shutdown
      ```

    - 常规配置：

      ```
      loglevel：配置日志级别，开发阶段配置debug，上线阶段配置notice或者warning。
      
      logfile：指定日志文件。redis在运行过程中，会输出一些日志信息：默认情况下，这些日志信息会输出到控制台，我们可以使用1ogfile配置日志文件，使redis把日志信息输出到指定文件中。
      
      databases：配置redis服务默认创建的数据库实例个数，默认值是16。
      ```

13. redis的持久化：redis提供持久化策略，在适当的时机采用适当手段把内存中的数据持久化到磁盘中，每次redis服务启动时，都可以把磁盘上的数据再次加载内存中使用。

    - RDB策略：在指定时间间隔内，redis服务执行指定次数的写操作，会自动触发一次持久化操作。

      - RDB策略是redis默认的持久化策略，redis服务开启时这种持久化策略就已经默认开启了。

        ```
        save <seconds> <changes>: 配置持久化策略
        dbfilename: 配置redis RDB持久化数据存储的文件
        dir: 配置redis RDB持久化文件所在目录
        ```

    - AOF策略：采用操作日志来记录进行每一次写操作，每次redis服务启动时，都会重新执行一边操作日志中的指令。（效率低，主要是弥补RDB策略）

14. redis的事务：允许把一组redis命令放在一起，把命令进行序列化，然后一起执行，保证部分原子性。

    - multi：用来标记一个事务的开始

      ```
      multi
      set k1 v1
      set k2 v2
      ```

    - exec：用来执行事务队列中所有的命令。

    - redis的事务只能保证部分原子性：

      - 如果一组命令中，有在压入事务队列过程中发生错误的命令，则本事务中所有的命令都不执行，能够保证事务的原子性。

        ```
        multi
        seta k3 v3  -->压入队列error
        set k4 v4
        exec
        ```

      - 如果一组命令中，在压入队列过程中正常，但是在执行事务队列命令时发生了错误，则只会影响发生错误的命令，不会影响其它命令行，不能保证事务的原子性。

        ```
        multi
        set k3 v3
        incr k1
        set k4 v4  -->执行事务队列error
        exec
        ```

    - discard：清除所有已经压入队列中的命令，并且结束整个事务。

      ```
      multi
      set k5 v5
      set k6 v6
      discard  --> err exec without multi
      exec
      ```

    - watch：监控某一个键，当事务在执行过程中，此键代码的值发生变化，则本事务放弃执行；否则，正常执行。

    - unwatch：放弃监控所有的键。

    - 事务小结：

      - 单独的隔离操作：事务中的所有命令都会序列化、顺序地执行。事务在执行过程中，不会被其它客户端发来的命令请求所打断，除非使用watch命令监控某些键。
      - 不保证事务的原子性：redis 同一个事务中如果一条命令执行失败，其后的命令仍然可能会被执行，redis 的事务没有回滚。Redis 已经在系统内部进行功能简化，这样可以确保更快的运行速度，因为Redis不需要事务回滚的能力。

15. redis消息的发布与订阅：redis客户端订阅频道，消息发布者往频道上发布消息，所有订阅此频道的客户端都能够接收到消息。

    - subscribe：订阅一个或多个频道的消息。
      - subscribe ch1 ch2 ch3
    - publish：将消息发布到指定频道
      - publish ch1 hello

16. redis的主从复制：主少从多、主写从读、读写分离、主写同步复制到从。（一个从机只能有一个主机）

    - 查看redis服务在集群中的主从角色：info replication

      - 默认情况下，所有的redis服务都是主机，即都能写和读，但是都还没有从机。

    - 设置主从关系：设从不设主

      ```
      假设有三台redis客户端，端口号分别是：6379，6380，6381
      在6380上执行：slaveof 127.0.0.1 6379 -->主机的ip地址和端口号
      ```

    - 全量复制：一旦主从关系确定，会自动把主机上已有的数据同步复制到从库。

    - 增量复制：主库写数据会自动同步到从库。

    - 主写从读，读写分离：在从机上写数据会报错，主机可以读也可以写，但是不建议主机上读。

    - 当主机宕机时，从机的状态从up变为down，还可读，但是不会更新数据；当主机重新连接时，从机状态为up。从机并不会因为主机的故障而发生改变。

    - 当从机宕机时，主机少一个从机，其它从机不变；从机恢复时，需要重新设置主从关系，否则为主机。

    - 从机上位：当主机故障无法修复时，需要指定一个性能较好的从机来代替原主机；步骤：

      1. 从机断开原来主从关系  --> slaveof no one (在从机上执行)
      2. 重新设置主从关系；

    - 小结：一台主机配置多台从机，一台从机又可以配置多台从机，从而形成一个庞大的集群架构。减轻一台主机的压力，但是增加了服务间的延迟时间。（只要有从的属性，就不能写）

17. redis的哨兵模式：

    - 启动哨兵服务：redis-sentinel redis_sentinel.conf
    - 当主机发生宕机时，哨兵自动选择最优的从机上位。
    - 当之前的主机恢复时，自动从属新的主机。
    - 哨兵模式的三大任务：监控、提醒、自动故障迁移。

18. redis的缺点：redis的主从复制最大的缺点就是延迟，主机负责写，从机负责备份，这个过程有一定的延迟，当系统很繁忙的时候，延迟问题会更加严重，从机数量的增加也会使这个问题更加严重。

19. Jedis：

    - 用Jedis操作redsi --> 在idea中创建Jedis对象：
      - Jedis jedis = new Jedis("host","port"); -->连接redis服务



------

## Nginx

**一、Nginx的概述：**

​	nginx是一款自由的、开源的、高性能的HTTP服务器和反向代理服务器；同时也是一个IMAP、POP3、SMTP代理服务器；nginx可以作为一个HTTP服务器进行网站的发布处理，另外nginx可以作为反向代理进行负载均衡的实现。

**二、Nginx的作用：**

​	1、作为 Web 服务器：相比 Apache，Nginx 使用更少的资源，支持更多的并发连接，体现更高的效率，这点使 Nginx 尤其受到虚拟主机提供商的欢迎。能够支持高达 50,000 个并发连接数的响应。

​	2、作为负载均衡服务器：Nginx 既可以在内部直接支持 Rails 和 PHP，也可以支持作为 HTTP代理服务器 对外进行服务。Nginx 用 C 编写, 不论是系统资源开销还是 CPU 使用效率都比 Perlbal 要好的多。

​	3、作为邮件代理服务器: Nginx 同时也是一个非常优秀的邮件代理服务器（最早开发这个产品的目的之一也是作为邮件代理服务器），Last.fm 描述了成功并且美妙的使用经验。

**三、常见问题：**

WEB服务器前端配置Nginx的好处是什么？
答：反向代理与负载均衡。

**四、什么是正向代理？**

​	比如我们想通过自己的计算机A访问一个国外网站B，直接访问不了，此时有一台服务器C，是可以访问B的，那么我们就可以通过C来访问B。C就叫做代理服务器。

​	正向代理特点：就是我们明确知道要访问哪个网站，比如这里就清楚是网站B。

**五、什么是反向代理？**

​	当我们有一个服务器集群时（假定每个服务器内容一样），并且此时我们通过一个代理服务器访问集群，注意，由于服务器内容是一样的，我们并不知道是哪一台服务器在为我们服务，这种代理就是反向代理。

**六、负载均衡**

负载均衡是通过反向代理实现的。用户访问会先访问到Nginx服务器，然后Nginx服务器再从服务器集群中选择压力较小的服务器，然后将该访问引向该服务器。

**七、Nginx基本命令**

```
启动Nginx：/usr/local/nginx/sbin/nginx -c /usr/local/nginx/cong/nginx.conf

查看Nginx状态：ps -ef | grep nginx

关闭nginx：
	kill -QUIT 主pid
		注意：master process为主pid，worker process为子pid
			 这种关闭方式会处理完请求后再关闭，称为优雅的关闭
	kill -TERM 主pid
		注意：这种关闭方式不管请求是否处理完成，直接关闭，比较暴力，称为快速的关闭
		
重启nginx：
	./nginx -s r
```

