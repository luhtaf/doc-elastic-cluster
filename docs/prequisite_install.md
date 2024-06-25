# Installing Elasticsearch Cluster

It is recomended to check the latest version of elasticsearch as you read this documentation. When this documentation is created, the latest version of elasticsearch is [8.12.2](https://www.elastic.co/downloads/past-releases/elasticsearch-8-12-2)

Note: It's recommended to always check the latest stable version of Elasticsearch before installation. You can find the latest version on the official [Elasticsearch downloads page](https://www.elastic.co/downloads/elasticsearch). As of this documentation's creation, the latest stable version is [8.12.2](https://www.elastic.co/downloads/past-releases/elasticsearch-8-12-2). Some function may not work because of different version.

## Prerequisites
This guide assumes you are using Ubuntu 22.04. Make sure your system is up-to-date before proceeding.

```sudo apt update && sudo apt upgrade -y```

## Installation Steps
The installation process involves setting up three main components:

* [<b>Master Node</b>](./master_node): This node coordinates activities within the cluster and manages its overall health.
* <b>Data Nodes</b>: These nodes store and manage the actual data indexed by Elasticsearch. You can have multiple data nodes for increased storage capacity and redundancy.
* <b>Kibana</b>: This is the visualization platform that allows you to interact with and analyze the data stored within the cluster.

<b>Important Note</b>: It's recommended to install the Elasticsearch cluster on separate machines for optimal performance and fault tolerance. 