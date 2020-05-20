# Mongo


sudo mongod --fork --logpath /var/log/mongo0.log --port 27017 --dbpath /var/lib/mongo --replSet rs0
sudo mongod --fork --logpath /var/log/mongo1.log --port 27018 --dbpath /var/lib/mongo1 --replSet rs0

in secondary mongod node
rs.slaveOk()