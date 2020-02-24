# Migration

_Created by Seokje Park at 2020.02.21_

keyword

- `mongodb to elasticsearch`
- `migratino`

We will sync mongoDB with Elasticsearch

## MongoDB upgrade 3.6 to 4.0

  I followed this [instructions](https://docs.mongodb.com/v4.0/tutorial/install-mongodb-on-amazon/).

  If you come out as below, you have succeeded.

  ```bash
  $ mongo
    rs0:PRIMARY> db.version()
    4.0.16
  ```

## Setup Replica set on a single machine

  Referenced [here](https://www.tutorialkart.com/mongodb/setup-mongodb-replica-set/).

  ```bash
  $ 
  $ sudo mongod --fork --logpath /var/log/mongod0.log --port 27017 --dbpath /var/lib/mongo --replSet rs0 # Start a mongod instance
  $ sudo mkdir -p /var/lib/mongodb1/ # Start another mongod instance
  $ sudo mongod --fork --logpath /var/log/mongod1.log --port 27018 --dbpath /var/lib/mongo1 --replSet rs0
  $ mongo
  $  > rs.initiate()
  $  > rs.add('localhost:27018') # { "ok"" 1 }
  $  > rs.status()
  ```  

  - `sudo killall -15 mongod`: Kill all mongod process. (Use it if you want to upgrade or restart mongod)
  - `--fork --logpath /var/log/mongod0.log`: Commands to Run mongod as Daemons.
  - `ps -edaf | grep mongo | grep -v grep`: Command to check the running mongod process.

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

## Setup monstache config

  More options can be found [here](https://rwynn.github.io/monstache-site/start/).

  `{Any path}/config.toml`
  ```toml 
  mongo-url = "mongodb://localhost:27018"
  elasticsearch-urls = ["http://{elasticsearch url}:9200"]
  elasticsearch-max-conns = 4
  elasticsearch-max-seconds = 5
  elasticsearch-max-bytes = 8000000

  namespace-regex = '^{dbname}\.{colname}$'
  change-stream-namespaces  = ["dbname}.{colname}"]

  gzip = true
  stats = false
  index-stats = true

  dropped-collections = false
  dropped-databases = false

  replay = false
  resume = true
  resume-write-unsafe = false
  resume-name = "default"
  verbose = true
  exit-after-direct-reads = false
  ```

  The above config needs futher investigation.

## Start Synchronize MonogoDB to Elasticsearch using monstache

  ```bash
  $ monstache -f config.toml # watch mode
  $ nohup monstache -f config.toml & # background process
  ```

## Security

When you apply Elasticsearch basic authentication later, you must make the following changes.

  ```bash
  $ sudo vi config.toml
    elasticsearch-user = "elastic"
    elasticsearch-password = "{elasticsearch-setup-passwords generated elastic password}"
  ```
  See more about elasticsearch security [Setting Elaticsearch and Kibana](./Elasticsearch#secure-elasticsearch).

## Reference site
- [Tutorial: Sync mongoDB with Elasticsearch](https://medium.com/@eldishnawy/tutorial-sync-mongodb-with-elasticsearch-fb43e9bc13ce)
- [5 Different ways to synchronize data from MongoDB to ElasticSearch](https://code.likeagirl.io/5-different-ways-to-synchronize-data-from-mongodb-to-elasticsearch-d8456b83d44f)
- [MongoDB to ElasticSearch Sync using Monstache](https://medium.com/@nehajirafe/mongodb-to-elasticsearch-sync-using-monstache-cfe1177594b6)