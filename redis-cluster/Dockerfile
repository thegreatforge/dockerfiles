# Dockerfile for Redis Cluster

# Base image
FROM redis:6.2-alpine

ENV CLUSTER_IP="127.0.0.1" 

# Create Redis directories for each node
RUN mkdir -p /redis-node1/data  /redis-node2/data /redis-node3/data /redis-node4/data /redis-node5/data  /redis-node6/data

# Copy Redis configuration files for each node
COPY redis-node-1.conf /redis-node1/redis.conf
COPY redis-node-2.conf /redis-node2/redis.conf
COPY redis-node-3.conf /redis-node3/redis.conf
COPY redis-node-4.conf /redis-node4/redis.conf
COPY redis-node-5.conf /redis-node5/redis.conf
COPY redis-node-6.conf /redis-node6/redis.conf


# Configuration for the Redis server
CMD ["sh", "-c", "\
    redis-server /redis-node1/redis.conf & \
    redis-server /redis-node2/redis.conf & \
    redis-server /redis-node3/redis.conf & \
    redis-server /redis-node4/redis.conf & \
    redis-server /redis-node5/redis.conf & \
    redis-server /redis-node6/redis.conf & \
    sleep 10 && \
    redis-cli --cluster create \
    $CLUSTER_IP:6371 $CLUSTER_IP:6372 $CLUSTER_IP:6373 \
    $CLUSTER_IP:6374 $CLUSTER_IP:6375 $CLUSTER_IP:6376 \
    --cluster-replicas 1 --cluster-yes &&\
    sleep infinity"]

# Expose ports
EXPOSE 6371 6372 6373 6374 6375 6376

# Command to build the docker image
# docker build -t redis-cluster .

# Command to run the docker container
# docker run -d -p 6371:6371 -p 6372:6372 -p 6373:6373 -p 6374:6374 -p 6375:6375 -p 6376:6376 -e CLUSTER_IP="127.0.0.1" --name redis-cluster redis-cluster