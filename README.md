# redis docker
docker-redis  
docker-compose编排redis主从，手动配置主从

docker-redis-cluster

docker-compose编排 

******手动搭建集群 ********

1.首先 准备节点 每个节点需要开启配置cluster-enabled yes，让 Redis 运行在集群模式下。

Redis-master	172.50.0.2	6391 -> 6391	master

Redis-master2	172.50.0.3	6392 -> 6392	master

Redis-master3	172.50.0.4	6393 -> 6393	master

redis-slave	  172.30.0.2	6394 -> 6394	Slave

redis-slave2	172.30.0.3	6395 -> 6395	Slave

redis-slave3	172.30.0.4	6396 -> 6396	Slave

2.节点握手
通过命令 cluster meet 127.0.0.1 6380 与其他节点握手作为一个完整的集群，需要主从节点，保证当它出现故障时可以自动进行故障转移。集群模式下，Reids 节点角色分为主节点和从节点。首次启动的节点和被分配槽的节点都是主节点，从节点负责复制主节点槽信息和相关的数据。
使用 cluster replicate {nodeId}命令让一个节点成为从节点。其中命令执行必须在对应的从节点上执行，将当前节点设置为 node_id 指定的节点的从节点
redis-cli -h 47.98.147.49 -p 6395  CLUSTER REPLICATE   0affa79edef47e10a0459832d279fe74467be98b

3.分配槽
 利用 bash 特性批量设置槽（slots），命令如下：
redis-cli -h 47.98.147.49  -p 6391  cluster addslots {0..5461}
redis-cli -h 47.98.147.49  -p 6392 cluster addslots {5462..10922}
redis-cli -h 47.98.147.49  -p  6393 cluster addslots {10923..16383}
