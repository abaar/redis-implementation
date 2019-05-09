# Redis Implementation & Master Slave Failover

## Jumpto

## Architecture
No | Name | IP | Deskripsi
---|---|---|---
1| redismaster | 192.168.32.232 | Redis Master (2GB RAM)
2| redisslave1 | 192.168.32.233 | Redis Slave 1 (1GB RAM)
3| redisslave2 | 192.168.32.234 | Redis Slave 2 (1GB RAM)

## Installation
To install Redis using Master Slave Replication, you need to install Redis-Server & Redis-Sentinel. The steps are :
### Install Required Tools
```
sudo apt-get update -y
sudo apt-get install build-essential tcl -y
sudo apt-get install libjemalloc-dev  -y
```

### Allow Redis Working Port
```
sudo ufw allow from redismaster
sudo ufw allow from redisslave1
sudo ufw allow from redisslave2
```

### Install Redis
All you need to install Redis is the step below, it'll take few minutes to install. You can install it anywhere with proper permission. In my case, i've installed it on `HOME`.
```
sudo curl -O http://download.redis.io/redis-stable.tar.gz
sudo tar xzvf redis-stable.tar.gz
cd redis-stable
sudo make
sudo make test
sudo make install
```
Done, easy isn't it?

## Configuration
Then, to have a master slave architecture on Redis, you need to config `redis.conf` as the configuration of the Redis Server and `sentinel.conf` will be in charge of the configuration of the Redis Sentinel, Redis Tool that allow Redis to do replication and failover.

### Redis Configuration
#### Master
There aren't many changes in Master `redis.conf`.
```
bind 127.0.0.1 192.168.32.232
protected-mode no
port 6379
logfile "/home/vagrant/redis-stable/redis.log" #this is where you want to save your redis-server log
```
#### Slave
Just like Master Configuration , but you need to add `slaveof MasterIP PORT` to tell the Cluster that the it is a slave of Master. 
```
bind 127.0.0.1 'SLAVE IP'
protected-mode no
port 6379
slaveof 192.168.32.232 6379
logfile "/home/vagrant/redis-stable/redis.log" #this is where you want to save your redis-server log
```

### Sentinel Configuration
#### Master & Slave
The most importan setting on `sentinel.conf` is `sentinel monitor mymaster 192.168.32.232 6379 2`. It means that the sentinel need to monitor Master with Quorum 2 or the quorum to point a new master is 2 Nodes.
```
protected-mode no
logfile "/home/vagrant/redis-stable/sentinel.log"
sentinel monitor mymaster 192.168.32.232 6379 2
sentinel down-after-milliseconds mymaster 5000
sentinel failover-timeout mymaster 10000
```

## Testing
### Basic Test
#### PING
```

```
### Failover
