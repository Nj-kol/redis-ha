
# Meaning of important properties :

**sentinel monitor <cluster_name> <master_host> <master_host> <quorum>**

  - Gives information about the name of the cluster and the master host & port
  - The quorum tells form many slaves are required to elect a master

  Ex - sentinel monitor redis-cluster 127.0.0.1 6380 2
       
**sentinel down-after-milliseconds <cluster_name> <milli_seconds>**

  - This is the time for which the master should not be reachable
  - After this time a vote is triggered to elect a new master node

  Ex- sentinel down-after-milliseconds redis-cluster 5000

  Here Sentinel waits for 5 seconds

**sentinel parallel-syncs redis-cluster <no_of_slaves>**

  - This configuration indicates the number of slaves that are reconfigured
    simultaneously to point to a new master

  - During this process the slaves will be unavailable to clients.
    Use a low parallel-syncs number to minimize the number of simultaneously 
    unavailable slaves
  
 Ex - sentinel parallel-syncs redis-cluster 1

**sentinel failover-timeout <cluster_name> <time_in_milli_seconds>**

  - The main purpose of the directive failover-timeout is to avoid a failover 
    to a master that has experienced issues in a short period of time

   For example, assume that there is a master, R1, with three slaves, R2, R3, and R4. 
   If the master experiences issues, the slaves need to elect a new master. Assume that R2 
   becomes the new master and R1 returns to the group as a slave. If R2 has issues and another
   new election must take place before failover-timeout is exceeded, R1 will not be part of 
   the possible nodes to be elected as the master

   Ex- sentinel failover-timeout redis-cluster 10000




