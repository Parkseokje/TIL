# Migration

_Created by Seokje Park at 2020.02.21_

keyword

- `mongodb to elasticsearch`
- `migratino`

We will sync mongoDB with Elasticsearch

## Install Golang-go

  ```bash
  $ sudo yum install golang
  $ go env # test
  ```

## Download Monstache & upzip

  ```bash
  $ wget -O /home/ec2-user/monstache.zip "https://github.com/rwynn/monstache/releases/download/v6.5.1/monstache-8e69a61.zip"
  $ unzip monstache.zip -d ./monstache
  ```

## Export your path to the .profile

  ```bash
  $ sudo vi ~/.basrhc
  ```

  Add the following lines

  ```bash
  PATH="/home/ec2-user/monstache/build/linux-amd64:$PATH"
  ```

  Test

  ```bash
  $ monstache -v
  6.5.1
  ```

## Mongo Replica set
  ```bash
  $ sudo mkdir -p /data/node1/
  $ sudo chown -R $USER /data/node1/
  $ mongod --port 27108 --dbpath /data/node1/ --replSet rs0 --smallfiles --oplogSize 128
  
  ```

## When stuck with mongod try it
  ```bash
  $ sudo mongod -f /etc/mongod.conf
  ```

## Reference site
- [Tutorial: Sync mongoDB with Elasticsearch](https://medium.com/@eldishnawy/tutorial-sync-mongodb-with-elasticsearch-fb43e9bc13ce)
- [5 Different ways to synchronize data from MongoDB to ElasticSearch](https://code.likeagirl.io/5-different-ways-to-synchronize-data-from-mongodb-to-elasticsearch-d8456b83d44f)