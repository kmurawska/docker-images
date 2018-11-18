```
version: '3'

networks:
  cassandra_network:

services:

  cassandra-node-1:
    container_name: cassandra-node-1
    hostname: cassandra-node-1
    image: cassandra-waitable
    environment:
      - CASSANDRA_CLUSER_NAME=cassandra_cluster
      - CASSANDRA_SEEDS=cassandra-node-1
    expose:
      - 8333
      - 7000 #intra-node communication
      - 7001 #TLS intra-node communication
      - 7199 #JMX
      - 9160 #thrift service
    ports:
      - 9042:9042 #CQL
    volumes:
      - /mnt/sda1/cassandra_cluster/node1/shm:/var/lib/cassandra
    networks:
      - cassandra_network

  cassandra-node-2:
    container_name: cassandra-node-2
    hostname: cassandra-node-2
    image: cassandra-waitable
    environment:
      - CASSANDRA_CLUSER_NAME=cassandra_cluster
      - CASSANDRA_SEEDS=cassandra-node-1
      - WAIT_FOR=cassandra-node-1;8333;READY
    expose:
      - 8333
      - 7000
      - 7001
      - 7199
      - 9160
    ports:
      - 19042:9042
    volumes:
      - /mnt/sda1/cassandra_cluster/node2/shm:/var/lib/cassandra
    depends_on:
      - cassandra-node-1
    networks:
      - cassandra_network
```