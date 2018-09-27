
# Notes

* Redis Sentinel became stable in Redis 2.8 in late 2013

* Redis Sentinel is a distributed system designed to automatically promote 
  a Redis slave to master if the existing master fails
  
* Sentinel does not distribute data across nodes since the master node has 
  all of the data and the slaves have a copy of the data
  — Sentinel is not a distributed data store

* The most common architecture contains an installation of 
  one Sentinel for each Redis server
  
* Sentinel is a separate process from the Redis server, and it listens on its own port

* A client always connects to a Redis instance, but it needs to query a Sentinel to
  find out what Redis instance it is going to connect to
  
* The sentinel configuration is rewritten every time a new master is elected 
  or a new sentinel or slave joins the group of instances

* parallel-syncs, which specifies the number of slaves that can be reconfigured 
  simultaneously to point to a new master.
 
  During this process the slaves will be unavailable to clients. 
  Use a low parallel-syncs number to minimize the number of simultaneously 
  unavailable slaves.

## Redis Sentinel & CAP theorem

* Redis Sentinel is not highly available under network partitions
  When the master is down, system cannot accept writes until a 
  new master is elected
  
* Redis Sentinel is not strongly consistent in a network partition scenario
* Data may be lost when a split-brain occurs

* Redis Sentinel solves the automatic failover problem of high availability,
  but it does not solve the problem of distributing data across multiple Redis instances
