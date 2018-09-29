
# Replication

* Replication means that while you write to a Redis instance (usually referred to as the
  master), it will ensure that one or more instances (usually referred to as the slaves)
  become exact copies of the master

* Redis 2.8 introduced asynchronous replication, which makes slaves periodically
  acknowledge the amount of data to be processed
  
* A master can have multiple slaves and slaves can also accept connections from other slaves

* There are three ways of making a Redis server instance a slave:
  
  • Add the directive slaveof IP PORT to the configuration file and start a Redis
    server using this configuration
	
  • Use the redis-server command-line option --slaveof IP PORT

  • Use the command SLAVEOF IP PORT

* Replicas are widely used for scalability purposes so that all read operations are
  handled by replicas and the master handles only write operations

* Persistence can be moved to the replicas so that the master does not perform disk
  I/O operations. 
 
  In this scenario, the master server needs to disable persistence,
  and it should not restart automatically for any reason; otherwise, it will restart
  with an empty dataset and replicate it to the replicas, making them delete all of
  their stored data.

* It is possible to improve data consistency guarantees by requiring a minimum
  number of replicas connected to the master server.

  In this way, all write operations are only executed in the master Redis server 
  if the minimum number of replicas are satisfied, along with their
  maximum replication lag (in seconds)

  However, this feature is still weak because it does not guarantee that 
  all replicas have accepted the write operations; it only guarantees that 
  there is a minimum number of replicas connected to the master

* The configurations use to set it up are min-slaves-to-write 
   and min-slaves-max-lag—they default to 0 and 10, respectively

* Replicas are very useful in a master failure scenario because they contain all of
  the most recent data and can be promoted to master
  
  Unfortunately, when Redis is running in single-instance mode, there is no 
  automatic failover to promote a slave to master
 
  All replicas and clients connected to the old master need 
  to be reconfigured with the new master

* The command SLAVEOF NO ONE converts a slave into a master instance, and it
  should be used in a failover scenario.

Note :

* Replicas are read-only by default, but this can be changed by setting the
* configuration slave-read-only to yes. This, however, is not recommended!

