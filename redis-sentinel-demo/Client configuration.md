
# Client Connection

## With Lettuce

* Dependencies :

	<dependencies>
	  <dependency>
		<groupId>io.lettuce</groupId>
		<artifactId>lettuce-core</artifactId>
		<version>5.0.1.RELEASE</version>
	  </dependency>
	</dependencies>

* Code :

      public static StatefulRedisConnection<String, String> getConnectionForSentinel(String masterHost,
			Integer masterPort, String clusterName, Map<String, Integer> hosts) {

		@SuppressWarnings("static-access")
		Builder builder = RedisURI.builder().sentinel(masterHost, masterPort, clusterName);
		for (Entry<String, Integer> host : hosts.entrySet()) {
			builder = builder.withSentinel(host.getKey(), host.getValue());
		}
		RedisURI redisUri = builder.build();
		RedisClient client = RedisClient.create(redisUri);
		StatefulRedisConnection<String, String> connection = client.connect();
		return connection;
	}


Refererences
=============
https://dzone.com/articles/high-availability-with-redis-sentinels-connecting
