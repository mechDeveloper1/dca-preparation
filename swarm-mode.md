# Getting started with swarm mode

[link to docker swarm-tutorial](https://docs.docker.com/engine/swarm/swarm-tutorial/)


### Set up

###### Three networked host machines
    docker-machine create manager1
    docker-machine create worker1
    docker-machine create worker2
    
    $ docker-machine ls
    NAME       ACTIVE   DRIVER       STATE     URL                         SWARM   DOCKER     ERRORS
    manager1   -        virtualbox   Running   tcp://192.168.99.100:2376           v18.09.6
    worker1    -        virtualbox   Running   tcp://192.168.99.101:2376           v18.09.6
    worker2    -        virtualbox   Running   tcp://192.168.99.102:2376           v18.09.6


### Create a swarm

1. Open a terminal and ssh into the machine where you want to run manager node. If you use Docker Machine, you can connect to it via SSH using the following command:
   
   ```docker-machine ssh manager1```
    
2. Run the following command to create a new swarm:
    ```
    docker swarm init --advertise-addr <manager1-ip>
    
    docker@manager1:~$ docker swarm init --advertise-addr 192.168.99.100
    Swarm initialized: current node (v8x9dfvnaq5jhmsp4icfihr7n) is now a manager.

    To add a worker to this swarm, run the following command:

        docker swarm join --token SWMTKN-1-49fv1wy119322rnwaktnflgdbxww0w2wrrt494c7gbsfa4lvoh-47ujeky40eoebiwoh7o02mx03 192.168.99.100:2377

    To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.
    ```

3. Run docker info to view the current state of the swarm:
   
   ```docker info``` 

    ```
    docker@manager1:~$ docker info
    Containers: 0
     Running: 0
     Paused: 0
     Stopped: 0
    Images: 0
    Server Version: 18.09.6
    Storage Driver: overlay2
     Backing Filesystem: extfs
     Supports d_type: true
     Native Overlay Diff: true
    Logging Driver: json-file
    Cgroup Driver: cgroupfs
    Plugins:
     Volume: local
     Network: bridge host macvlan null overlay
     Log: awslogs fluentd gcplogs gelf journald json-file local logentries splunk syslog
    Swarm: active
     NodeID: v8x9dfvnaq5jhmsp4icfihr7n
     Is Manager: true
     ClusterID: x9ac70jqkgt1mqzzet9sldpfl
     Managers: 1
     Nodes: 1
     Default Address Pool: 10.0.0.0/8
     SubnetSize: 24
     Orchestration:
      Task History Retention Limit: 5
     Raft:
      Snapshot Interval: 10000
      Number of Old Snapshots to Retain: 0
      Heartbeat Tick: 1
      Election Tick: 10
     Dispatcher:
      Heartbeat Period: 5 seconds
     CA Configuration:
      Expiry Duration: 3 months
      Force Rotate: 0
     Autolock Managers: false
     Root Rotation In Progress: false
     Node Address: 192.168.99.100
     Manager Addresses:
      192.168.99.100:2377
    Runtimes: runc
    Default Runtime: runc
    Init Binary: docker-init
    containerd version: bb71b10fd8f58240ca47fbb579b9d1028eea7c84
    runc version: 2b18fe1d885ee5083ef9f0838fee39b62d653e30
    init version: fec3683
    Security Options:
     seccomp
      Profile: default
    Kernel Version: 4.14.116-boot2docker
    Operating System: Boot2Docker 18.09.6 (TCL 8.2.1)
    OSType: linux
    Architecture: x86_64
    CPUs: 1
    Total Memory: 989.4MiB
    Name: manager1
    ID: KGF2:BUCY:QZA4:OOQ2:74ES:HOY4:KGYD:J5UH:VIUS:2IPS:W2DE:AWJJ
    Docker Root Dir: /mnt/sda1/var/lib/docker
    Debug Mode (client): false
    Debug Mode (server): false
    Registry: https://index.docker.io/v1/
    Labels:
     provider=virtualbox
    Experimental: false
    Insecure Registries:
     127.0.0.0/8
    Live Restore Enabled: false
    Product License: Community Engine
    ```
4. Run the docker node ls command to view information about nodes:
   
   ```docker node ls```
    ```
    docker@manager1:~$ docker node ls
    ID                            HOSTNAME            STATUS              AVAILABILITY        MANAGER STATUS      ENGINE VERSION
    v8x9dfvnaq5jhmsp4icfihr7n *   manager1            Ready               Active              Leader              18.09.6
    ```
    
### Add nodes to the swarm
### Deploy a service
### Inspect the service
### Scale the service
### Delete the service
### Apply rolling updates
### Drain a node
### User swarm mode routing mesh
