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

#### Change in solr  

/solr-8.7.0/bin/solr.in.sh - ZK_HOST="172.17.0.6:2181,172.17.0.4:2181,172.17.0.5:2181" (As per the ip address of the zookeeper machines)

* if not working try killing 2181 with lsof -i:2181 command in zookeeper
 
