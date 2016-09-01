---
published: true
title: Elastic Search安装与优化
layout: post
---
##Installation

Install OpenJDK 8 on 14.04 LTS

    sudo add-apt-repository ppa:webupd8team/java -y
    sudo apt-get update
    sudo apt-get install oracle-java8-set-default

Download the latest stable version `elastic search`

    wget https://download.elastic.co/elasticsearch/release/org/elasticsearch/distribution/tar/elasticsearch/2.4.0/elasticsearch-2.4.0.tar.gz

Install plugins

    sudo bin/plugin install analysis-smartcn    # an analyzer for Chinese or mixed Chinese-English text.
    sudo bin/plugin install delete-by-query     # query delete api
    sudo bin/plugin install license             # license
    sudo bin/plugin install shield              # security

Update license, [link](https://www.elastic.co/guide/en/marvel/current/license-management.html)

    curl -XPUT -u admin 'http://<host>:<port>/_license' -d @license.json

Set heap size

    export ES_HEAP_SIZE=6g
    
Disable swap, add below command to `/etc/fstab`

    sudo swapoff -a
    
Check `max_file_descriptors`

    http://<host>:<port>/_nodes/stats/process?pretty

##Production Deployment


###Memory

**A machine with 64 GB of RAM is the ideal sweet spot**, but 32 GB and 16 GB machines are also common. Less than 8 GB tends to be counterproductive (you end up needing many, many small machines), and greater than 64 GB has problems that we will discuss in Heap: Sizing and Swapping.

###CPUs

**Most Elasticsearch deployments tend to be rather light on CPU requirements**. As such, the exact processor setup matters less than the other resources. You should choose a modern processor with multiple cores. Common clusters utilize two- to eight-core machines.

**If you need to choose between faster CPUs or more cores, choose more cores**. The extra concurrency that multiple cores offers will far outweigh a slightly faster clock speed.


###Disks

If you can afford SSDs, they are by far superior to any spinning media. SSD-backed nodes see boosts in both query and indexing performance. **If you can afford it, SSDs are the way to go**.

Check I/O Scheduler, **TODO**

###Network

A fast and reliable network is obviously important to performance in a distributed system. Low latency helps ensure that nodes can communicate easily, while high bandwidth helps shard movement and recovery. **Modern data-center networking (1 GbE, 10 GbE) is sufficient for the vast majority of clusters**.

**Avoid clusters that span multiple data centers, even if the data centers are colocated in close proximity**. Definitely avoid clusters that span large geographic distances.

###General Considerations

**In general, it is better to prefer medium-to-large boxes**. Avoid small machines, because you don’t want to manage a cluster with a thousand nodes, and the overhead of simply running Elasticsearch is more apparent on such small boxes.


###Java Virtual Machine

**You should always run the most recent version of the Java Virtual Machine (JVM), unless otherwise stated on the Elasticsearch website**. Elasticsearch, and in particular Lucene, is a demanding piece of software. The unit and integration tests from Lucene often expose bugs in the JVM itself. These bugs range from mild annoyances to serious segfaults, so it is best to use the latest version of the JVM where possible.

**Java 8 is preferred over Java 7**. Java 6 is no longer supported.

**Please Do Not Tweak JVM Settings**. The JVM exposes dozens (hundreds even!) of settings, parameters, and configurations. They allow you to tweak and tune almost every aspect of the JVM.

###Transport Client Versus Node Client

If you are using Java, you may wonder when to use the transport client versus the node client.

**The transport client is ideal if you want to decouple your application from the cluster**. For example, if your application quickly creates and destroys connections to the cluster, a transport client is much "lighter" than a node client, since it is not part of a cluster.

On the flipside, **if you need only a few long-lived, persistent connection objects to the cluster, a node client can be a bit more efficient since it knows the cluster layout**. But it ties your application into the cluster, so it may pose problems from a firewall perspective.

###Configuration Management

If you use configuration management already (Puppet, Chef, Ansible), you can skip this tip.

**TODO**

###Important Configuration Changes

Elasticsearch ships with very good defaults, especially when it comes to performance- related settings and options. **When in doubt, just leave the settings alone**.

    cluster.name: elasticsearch_production
    node.name: elasticsearch_005_data
    path.data: /path/to/data1
    path.logs: /path/to/logs
    path.plugins: /path/to/plugins


###Heap: Sizing and Swapping

**The standard recommendation is to give 50% of the available memory to Elasticsearch heap, while leaving the other 50% free**. It won’t go unused; Lucene will happily gobble up whatever is left over.

There is another reason to not allocate enormous heaps to Elasticsearch. As it turns out, **the HotSpot JVM uses a trick to compress object pointers when heaps are less than around 32 GB**.

**It should be obvious, but it bears spelling out clearly: swapping main memory to disk will crush server performance**. Think about it: an in-memory operation is one that needs to execute quickly.

###File Descriptors and MMap

**You should increase your file descriptor count to something very large, such as 64,000**. This process is irritatingly difficult and highly dependent on your particular OS and distribution. Consult the documentation for your OS to determine how best to change the allowed file descriptor count.

##Reference

Basic Concepts
> https://www.elastic.co/guide/en/elasticsearch/reference/current/_basic_concepts.html

Production deployment, hardware
> https://www.elastic.co/guide/en/elasticsearch/guide/current/hardware.html

When do you start additional Elasticsearch nodes
> http://stackoverflow.com/questions/12409438/when-do-you-start-additional-elasticsearch-nodes