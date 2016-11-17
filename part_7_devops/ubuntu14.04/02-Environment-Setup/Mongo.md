# 安装mongodb
https://www.digitalocean.com/community/tutorials/how-to-install-mongodb-on-ubuntu-14-04
https://docs.mongodb.com/v3.2/tutorial/install-mongodb-on-ubuntu/

## 	Import the public key used by the package management system.

```bash
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
```

## Create a list file for MongoDB.

```bash
# Ubuntu 14.04
echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
```

## 	Reload local package database.

```bash
sudo apt-get update
```

## Install the MongoDB packages.
```bash
sudo apt-get install -y mongodb-org
```

## Start & Stop & restart MongoDB

```bash
# start 
sudo service mongod start

# stop 
sudo service mongod stop  

# restart
sudo service mongod restart 
```

查看mongod运行状态

```bash
service mongod status 
```


## Uninstall MongoDB
### Stop MongoDB.

Stop the mongod process by issuing the following command:

```bash 
sudo service mongod stop
```

Remove Packages.

Remove any MongoDB packages that you had previously installed.

```bash 
sudo apt-get purge mongodb-org*
```
Remove Data Directories.

Remove MongoDB databases and log files.

```bash 
sudo rm -r /var/log/mongodb
sudo rm -r /var/lib/mongodb
```