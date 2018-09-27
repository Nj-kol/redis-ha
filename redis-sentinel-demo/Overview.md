
## Redis Sentinel
 
* When a master node experiences issues, one of its slave nodes needs to be
  promoted to master, and all the other slaves need to be reconfigured to point to
  the new master
 
  Before Redis Sentinel, this failover process was done manually,
  which was not very reliable.
 
* Redis Sentinel is a distributed system designed to automatically promote 
  a Redis slave to master if the existing master fails

* Sentinel does not distribute data across nodes since the master node has 
  all of the data and the slaves have a copy of the data
  — Sentinel is not a distributed data store
  
* The most common architecture contains an installation of one Sentinel 
  for each Redis server
  
* Sentinel is a separate process from the Redis server, and it listens on its own port

* The major difference when using Redis Sentinel is that it implements a different
  interface, which may require you to install a Redis client that supports Sentinel.

  A client always connects to a Redis instance, but it needs to query a Sentinel to
  find out what Redis instance it is going to connect to

* When you download Redis, it comes with a configuration file for Sentinel,
  called sentinel.conf

* In the initial configuration, only the master nodes need to be listed.

* All slaves are found when Sentinel starts and asks the masters where their slaves
  are. The Sentinel configuration will be rewritten as soon as the Sentinel finds all
  the available slaves, or when a failover occurs.

* Communication between all Sentinels takes place through a Pub/Sub channel
  called __sentinel__:hello in the Redis master
