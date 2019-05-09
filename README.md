# Redis Implementation & Master Slave Failover

## Jumpto

## Architecture

## Installation
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
```
sudo curl -O http://download.redis.io/redis-stable.tar.gz
sudo tar xzvf redis-stable.tar.gz
cd redis-stable
sudo make
sudo make test
sudo make install
```


## Configuration

### Redis Configuration
#### Master
```
bind 127.0.0.1 192.168.32.232
protected-mode no
port 6379
logfile "/home/vagrant/redis-stable/redis.log" #this is where you want to save your redis-server log
```
#### Slave
```
bind 127.0.0.1 'SLAVE IP'
protected-mode no
port 6379
slaveof 192.168.32.232 6379
logfile "/home/vagrant/redis-stable/redis.log" #this is where you want to save your redis-server log
```

### Sentinel Configuration
#### Master & Slave
```
protected-mode no
logfile "/home/vagrant/redis-stable/sentinel.log"
sentinel monitor mymaster 192.168.32.232 6379 2
sentinel down-after-milliseconds mymaster 5000
sentinel failover-timeout mymaster 10000
```
