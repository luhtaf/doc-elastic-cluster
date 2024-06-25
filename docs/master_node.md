# Installing Master Node


## Download Installer
First, we need to dowload Elasticsearch just as previous mentioned

```
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-8.12.2-amd64.deb
```

Please make sure to adjust to the latest version as you proceed.

## Install
Install the downloaded package using `dpkg`:

```
dpkg -i https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-8.12.2-amd64.deb
```

In this step, there will be username and password for your elasticsearch instance like following:

```
The generated password for the elastic built-in superuser is : "password"
```


or you can manually add new user with command and add the roles: (optional)
```
/usr/share/elasticsearch/bin/elasticsearch-users useradd {new user}
/usr/share/elasticsearch/bin/elasticsearch-users roles {new user} -a superuser
```

## Configure Master Node
Configure master node in `/etc/elasticsearch/elasticsearch.yml` like following:

```
cluster.name: "cluster name"
node.name: "node name"
node.roles: [data, master]
discovery.seed_hosts: ["ip master","ip data"]
cluster.initial_master_nodes: ["ip master"]
network.host: 0.0.0.0
```

* <b>cluster.name</b>: your prefered cluster name (it must be same in all nodes in 1 cluster)
* <b>node.name</b>: your prefered node name (it must unique for all node in 1 cluster)
* <b>node.roles</b>: the role for current elasticsearch [role](https://www.elastic.co/guide/en/elasticsearch/reference/current/modules-node.html#node-roles)
* <b>discovery.seed_host</b>: list of initial ip or domain of nodes in cluster
* <b>cluster.initial_master_nodes</b>: list ip of master nodes in cluster
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