
# Redis HA

* In Redis there are three modes in which you can 
  have some degree of high availability
  
**1. Async replication**
  - One master many slaves
  - No automatic failover
  - No sharding
  
**2. Redis Sentinel**
  - One master many slaves
  - Automatic failover possible
  - No sharding
  
**3. Redis Cluster**
  - Multiple master, multiple slaves
  - Automatic failover possible
  - Sharding possible
