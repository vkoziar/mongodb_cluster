# mongodb_cluster
# Use Ubuntu14.04x64

sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates
sudo apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
sudo /etc/apt/sources.list.d/docker.list
sudo vim /etc/apt/sources.list.d/docker.list
apt-cache policy docker-engine
sudo apt-get install docker-engine
sudo service docker start
sudo docker pull treasureboat/centos6
mkdir mongo
cd mongo/
mkdir  mongod
cd mongod/
vim Dockerfile
sudo docker build   -t dev24/mongodb mongod
mkdir mongos
cd mongos
vim Dockerfile
sudo docker build   -t dev24/mongos mongos
sudo docker run -P --name rs1_srv1 -d dev24/mongodb --replSet rs1 --noprealloc --smallfiles
sudo docker run -P --name rs1_srv2 -d dev24/mongodb --replSet rs1 --noprealloc --smallfiles
sudo docker run -P --name rs1_srv3 -d dev24/mongodb --replSet rs1 --noprealloc --smallfiles
sudo docker run -P --name rs2_srv1 -d dev24/mongodb --replSet rs2 --noprealloc --smallfiles
sudo docker run -P --name rs2_srv2 -d dev24/mongodb --replSet rs2 --noprealloc --smallfiles
sudo docker run -P --name rs2_srv3 -d dev24/mongodb --replSet rs2 --noprealloc --smallfiles
sudo docker inspect rs1_srv1
sudo docker inspect rs1_srv1 | grep port
sudo docker inspect rs1_srv1 | grep ort
sudo apt-get install mongodb-clients
mongo 172.17.0.2:27017

sudo docker inspect rs1_srv1 | grep IP
sudo docker inspect rs1_srv2 | grep IP
sudo docker inspect rs1_srv3 | grep IP
mongo 172.17.0.2:27017

sudo docker inspect rs2_srv1 | grep IP
mongo 172.17.0.5:27017
sudo docker inspect rs2_srv2 | grep IP
sudo docker inspect rs2_srv3 | grep IP
mongo 172.17.0.5:27017
mongo 172.17.0.2:27017
sudo docker inspect rs1_srv1 | grep IP
sudo docker inspect rs1_srv2 | grep IP
sudo docker inspect rs1_srv3 | grep IP
mongo 172.17.0.2:27017

sudo docker run  -P --name cfg1 -d dev24/mongodb   --noprealloc --smallfiles   --configsvr   --dbpath /data/db   --port 27017
sudo docker run  -P --name cfg2 -d dev24/mongodb   --noprealloc --smallfiles   --configsvr   --dbpath /data/db   --port 27017
sudo docker run  -P --name cfg3 -d dev24/mongodb   --noprealloc --smallfiles   --configsvr   --dbpath /data/db   --port 27017

sudo docker run -P --name mongos1 -d dev24/mongos --port 27017 --configdb 172.17.0.8:27017,172.17.0.9:27017,172.17.0.10:27017

https://sebastianvoss.com/docker-mongodb-sharded-cluster.html


