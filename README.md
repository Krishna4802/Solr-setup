# Solr-setup

## Basic installations :

    * apt update
    * apt install default-jre
    * apt-get install wget
    * apt install nano
    * apt install sudo
    * apt install vim


## To Download Solr-8.11.2 and extract :

    * wget https://archive.apache.org/dist/lucene/solr/8.11.2/solr-8.11.2.tgz
    * tar -xzf solr-8.11.2.tgz


## To Download and Zookeeper :

    * wget https://archive.apache.org/dist/zookeeper/zookeeper-3.4.6/zookeeper-3.4.6.tar.gz
    * tar -xzf zookeeper-3.4.6.tar.gz


## After this start solr :

    * cd solr-8.11.2
    * bin/solr -e cloud -force

## Then Execute the following command to enable security :

    * bin/solr auth enable -type basicAuth -prompt true -z localhost:9983 -blockUnknown true
                Here it will ask for admin name and password 	


## once set go to Solr UI

<img width="1293" alt="Pasted Graphic 1" src="https://github.com/Krishna4802/Solr-setup/assets/139359113/cd854a7e-6e13-406b-adcb-d2740463526e">


### * Then go to “add role” column and create a new role  

Here all, collection-admin-read, config-read, core-admin-read needs to be enabled to give the users only the read access 

<img width="1295" alt="Screenshot 2023-11-28 at 1 34 38 PM" src="https://github.com/Krishna4802/Solr-setup/assets/139359113/b74aeaaa-4d12-46f6-bbea-8f4a55b68caf">

### * Once the role is created, verify the permissions tab to confirm whether new role have necessary permissions  

<img width="1285" alt="Screenshot 2023-11-28 at 1 35 26 PM" src="https://github.com/Krishna4802/Solr-setup/assets/139359113/49b667ea-f3bb-4caf-a4dc-ac25b2eb5354">

### * Then go for creating of user  

<img width="1295" alt="Screenshot 2023-11-28 at 1 35 51 PM" src="https://github.com/Krishna4802/Solr-setup/assets/139359113/6d747ca7-8b6b-499c-8ea9-c0fb82fd88f6">

### * Then we can login with the role: 

<img width="1294" alt="Screenshot 2023-11-28 at 1 36 22 PM" src="https://github.com/Krishna4802/Solr-setup/assets/139359113/57f0c0e8-bd85-4899-8cfa-63b9325d3293">

 

## Now ACL setup

    * cd zookeeper-3.4.6/bin
    * ./zkServer.sh start /zookeeper-3.4.6/conf/zoo_sample.cfg   - to start zookeeper
    * ./zkServer.sh status /zookeeper-3.4.6/conf/zoo.cfg  - to check status of zookeeper
    * ./zkCli.sh -server localhost:2181 - execute this command to get into zookeeper 
    
    inside Zookeeper terminal
            * ls /   - to list 
            * getAcl /   - for listing acl for that directory
            * setAcl / world:anyone:r,ip:172.17.0.2:cdwra    - for setting the ips

            
## Zookeeper - Zoo.cfg file

* Add folder named with myid file and id of zk should be mentioned like 1 or 2 or 3 (this directory location should be given in dataDir= in the file )
    
      # The number of milliseconds of each tick
      tickTime=2000
      # The number of ticks that the initial 
      # synchronization phase can take
      initLimit=10
      # The number of ticks that can pass between 
      # sending a request and getting an acknowledgement
      syncLimit=5
      # the directory where the snapshot is stored.
      # do not use /tmp for storage, /tmp here is just 
      # example sakes.
      dataDir=/data
      # the port at which the clients will connect
      clientPort=2181
      4lw.commands.whitelist=mntr,conf,ruok
      
      # the maximum number of client connections.
      # increase this if you need to handle more clients
      #maxClientCnxns=60
      server.1=172.17.0.6:2888:3888
      server.2=172.17.0.4:2889:3889
      server.3=172.17.0.5:2899:3899
      # Be sure to read the maintenance section of the 
      # administrator guide before turning on autopurge.
      #
      # https://zookeeper.apache.org/doc/current/zookeeperAdmin.html#sc_maintenance
      #
      # The number of snapshots to retain in dataDir
      #autopurge.snapRetainCount=3
      # Purge task interval in hours
      # Set to "0" to disable auto purge feature
      #autopurge.purgeInterval=1
      
      ## Metrics Providers
      #
      # https://prometheus.io Metrics Exporter
      #metricsProvider.className=org.apache.zookeeper.metrics.prometheus.PrometheusMetricsProvider
      #metricsProvider.httpHost=0.0.0.0
      #metricsProvider.httpPort=7000
      #metricsProvider.exportJvmInfo=true
***

### Zookeeper Commands
      /bin/zkServer.sh start
      /bin/zkServer.sh status
      /bin/zkServer.sh stop


#### Change in solr  

/solr-8.7.0/bin/solr.in.sh - ZK_HOST="172.17.0.6:2181,172.17.0.4:2181,172.17.0.5:2181" (As per the ip address of the zookeeper machines)

* if not working try killing 2181 with lsof -i:2181 command in zookeeper
 
