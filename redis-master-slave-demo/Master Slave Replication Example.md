
# Master Slave

## Three Redis instances: One master and two replicas.

* On the first terminal, start the master redis-server on port 5555 :

  $ redis-server --port 5555
 
* On the second terminal, start the first slave on port 6666 :

  $ redis-server --port 6666 --slaveof 127.0.0.1 5555
 
* On the third terminal, start the second slave on port 7777 :

  $ redis-server --port 7777 --slaveof 127.0.0.1 5555

* At this point, there is a master with two replicas running.

* On the fourth terminal, check whether the replication is working:

	redis-cli -p 5555 SET testkey testvalues
	redis-cli -p 6666 GET testkey
	redis-cli -p 7777 GET testkey

## Master crash

* Assumes there is a master on port 5555 and there are two slaves
  on ports 6666 and 7777, respectively

  If the master instance is offline (crashed or maintenance window), 
  it may be required that one of its replicas become a master. 
  
  In this situation, all connected replicas and clients need to be reconfigured
  
* The following snippet causes a crash in the master instance (port 5555), configures
  one of the slaves to become a master, and reconfigures the second slave to replicate
  the new master:

  $ redis-cli -p 5555 DEBUG SEGFAULT
  $ redis-cli -p 6666 SLAVEOF NO ONE
  $ redis-cli -p 7777 SLAVEOF 127.0.0.1 6666

* Check the new replication configuration is working:

  $ redis-cli -p 6666 SET newkey newvalue
  
  $ redis-cli -p 7777 GET newkey
  
  In the previous scenario, all clients that were connected to 
  127.0.0.1:5555 need to be reconfigured to connect to 127.0.0.1:6666
  
  
  
