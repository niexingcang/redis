# redis docker
docker-redis  
docker-compose编排redis主从，手动配置主从

docker-redis-cluster
docker-compose编排 手动搭建集群 
1.首先 准备节点 每个节点需要开启配置cluster-enabled yes，让 Redis 运行在集群模式下。
Redis-master	172.50.0.2	6391 -> 6391	master

Redis-master2	172.50.0.3	6392 -> 6392	master

Redis-master3	172.50.0.4	6393 -> 6393	master

redis-slave	  172.30.0.2	6394 -> 6394	Slave

redis-slave2	172.30.0.3	6395 -> 6395	Slave

redis-slave3	172.30.0.4	6396 -> 6396	Slave
2.节点握手
3.分配槽
