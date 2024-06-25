# Installing Master Node
This page tell how to add 1 data node to existing elasticsearch cluster

## Download Installer
First, dowload Elasticsearch like previous node

```
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-8.12.2-amd64.deb
```

Please make sure to adjust to the latest version as you proceed.

## Install
Install the downloaded package using `dpkg`:

```
dpkg -i https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-8.12.2-amd64.deb
```

like last step, there will be username and password for your elasticsearch instance like following:

```
The generated password for the elastic built-in superuser is : "password"
```


## Generate enrollment token 
An enrollment token is used by data node to identify the master node. (do it in master node)

```
/usr/share/elasticsearch/bin/elasticsearch-create-enrollment-token –s node
```

this step will produce a token that will used to reconfigure data node

## Reconfigure data node
reconfigure the data node to identify the master node using enrollment token generated from last step with command:

```
/usr/share/elasticsearch/bin/elasticsearch-reconfigure-node --enrollment-token "token"
```

## Configure Data Node
Configure data node in `/etc/elasticsearch/elasticsearch.yml` like following:

```
    cluster.name: "cluster name"
    node.name: "node data"
    node.roles: [data]
    cluster.initial_master_nodes: ["ip master"]
    network.host: 0.0.0.0
```

* <b>cluster.name</b>: your prefered cluster name (it must be same in all nodes in 1 cluster)
* <b>node.name</b>: your prefered node name (it must unique for all node in 1 cluster)
* <b>cluster.initial_master_nodes</b>: list ip of master nodes in cluster
* <b>node.roles</b>: the role for current elasticsearch [role](https://www.elastic.co/guide/en/elasticsearch/reference/current/modules-node.html#node-roles)
* <b>network.host</b>: ip of this node (leave it to 0.0.0.0 if you have multiple ip in 1 machine)


## Configure Firewall
allow port 9200 and 9300 so data node can access the master node:

```
iptables -I INPUT -p tcp --dport 9200 -j ACCEPT
iptables -I INPUT -p tcp --dport 9300 -j ACCEPT
```

## Start your elasticsearch Instance
start elasticsearch service in master node with command:

```
systemctl start elasticsearch
```

## Additional
