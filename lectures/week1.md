# Week 1 lectures

## Course Schedule
| **Week** | **Topic**                                                      | **Lab**                    | **Assignment** |
|----------|----------------------------------------------------------------|----------------------------|----------------|
| 1        | Course info and introduction to big data + Hadoop, HDFS and YARN | Hadoop setup HDFS practice |                |
| 2        | Hadoop MapReduce 1                                             | MapReduce                  |                |
| 3        | Hadoop MapReduce 2                                             | MapReduce                  |                |
| 4        | Spark 1                                                        | MapReduce                  | Project 1 due  |
| 5        | Spark 2                                                        | Spark                      |                |
| 6        | Flex week                                                      |                            |                |
| 7        | Finding similar items                                          | Spark                      | Project 2 due  |
| 8        | Streaming data mining                                          | Spark                      |                |
| 9        | NoSQL, HBase and Hive                                          | High level MapReduce tools |                |
| 10       | TBA/Revisions                                                  | Real cloud platform        | Project 3 due  |

## Introduction to Big Data
### What is Big Data?
* Big data is a field tyhat treats ways to analyse, systemetically extract informtion from, or otherwise deal with data sets that are **too large or complex** to be dealt with by *traditional data-processing* application software
* Challenges include:
  * Capturing data
  * Data storage
  * Data analysis
  * Search
  * Sharing
  * Transfer
  * Visualisation
  * Querying
  * Updating
  * Information privacy
  * Data source
* 'Big data' refers to the use of predictive analytics, user behaviour analytics, or certain other advanced data analytics methods that extract value from big data, and seldom to a particular size of data set
* Crowded application ecosystem:
  * Hadoop MapReduce
  * Spark
  * High-level query languages (Hive)
  * NoSQL (e.g., HBase, MongoDB, Neo4j)
  * Pregel
  * Flink
* Data science and data management
  * Finding similar items
  * Graph data processing
  * Streaming data processsing
* Who is generating Big data?
  * Social media
  * User track + engagement
  * Homeland security
  * eCommerce
  * Financial services
  * Real-time search

### Big Data characteristics (3V and more)
| **3V Characteristics**     | **Definition**                                                                                                                                                                            | **Example**                                                                                                                                                                                                     |
|----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Volume (scale)             | The amounts of data collected and processed are much larger than those stored in typical relational databases                                                                             | Data volume is increasing exponentially (40% increase per year)                                                                                                                                                 |
| Variety                    | Big data consists of a rich variety of data types                                                                                                                                         | Relational data (tables/transaction/legacy data), text data (web), semi-structured data (XML), spatial data, temporal data, graph data (social network, sematic web (RDF)) and different sources e.g., reviews  |
| Velocity                   | Big data arrives to the organisation at high speeds and from multiple sources simultaneously. Velocity measures how fast the data is coming in                                            | Online data analytics e.g., e-promotions based on location, healthcare monitoring devices, contact tracing for COVID-19 cases and predicting future hotspots                                                    |
| **Other characteristics**  |                                                                                                                                                                                           |                                                                                                                                                                                                                 |
| Veracity (quality & trust) | Data = quantity + quality. Can we trust the answers to our queries to make the right decisions                                                                                            | Misleading financial reports can lead to loss of revenue, credibility, customers and disastrous consequences                                                                                                    |
| Value                      | Big data is meaningless if it does not provide value toward some meaningful goal                                                                                                          |                                                                                                                                                                                                                 |
| Visibility                 | The state of being able to see or be seen is implied                                                                                                                                      | Big data - visibility = black hole?                                                                                                                                                                             |
| Visualisation              | Making all the vast amount of data comprehensible in a manner that is easy to understand and read                                                                                         | BI/visualisation/analytics tools                                                                                                                                                                                |
| Variability                | Data whose meaning is constantly changing particular when gathering data relies on language processing. It defines the need to get meaningful data considering all possible circumstances |                                                                                                                                                                                                                 |
| Viscosity                  | The latency or lag time in the data relative to the event being described                                                                                                                 |                                                                                                                                                                                                                 |
| Volatility                 | How long is data valid and how long should it be stored. You need to determine at what point is data no longer relevant to the current analysis                                           |                                                                                                                                                                                                                 |

* Big data
  * Volume (data at rest): terabytes to exabytes of existing data to process
  * Velocity (data in motion): streaming data, milliseconds to seconds to respond
  * Variety (data in many forms): structured, unstructured, text, multimedia
  * Veracity (data in doubt): uncertainty due to data inconcsistency & incompleteness, ambiguities, latency, deception, model approximations
* Open data
  * Visbility (data in the open): open data is generally open to anyone which raises issues of privacy, security and provenance
  * Value (data of many values): large range of data values from free (data philanthropy) to high value monetisation

## Hadoop
* Distributed processing is non-trivial
  * How to assign tasks to different workers in an effective way?
  * What happens if tasks fail?
  * How do workers exchange results?
  * How to synchronise distributed tasks allocated to different workers?
* Big data storage is challenging
  * Data volumes are massive (e.g. even a single document can’t be stored on one machine)
  * Reliability of storing PBs of data is challenging
  * All kinds of failure: disk/hardware/network failures
  * Probability of failures simply increase with the number of machines
* What is Hadoop
  * Open-source data storage and processing platform
  * Before the advent of Hadoop, storage and processing of big data was a big challenge
  * Massively scalable, automatically parallelizable
    * Based on work from Google
      * Google: GFS, MapReduce, BigTable (not open sourced)
      * Hadoop: HDFS, Hadoop MapReduce, HBase (open-sourced)
  * Named by Doug Cutting in 2006
* Hadoop offers
  * Redundant, fault-tolerant data storage
  *	Parallel computation framework
  *	Job coordination 	
* Why use Hadoop
  *	Cheaper -> scales to PB or more easily
  * Faster -> parallel data processing
  *	Better -> suited for types of big data problems
* Common Hadoop Distributions
  * Open source
    * Apache
  * Commercial
    * Cloudera
    * Hortonworks
    * MapR
    * AWS MapReduce
    * Microsoft Azure

## HDFS
### File system
* A ***filesystem*** is the methods and data structures that an operating system uses to keep track of files on a disk or partition; that is, the way files are organised on the disk

### Latency and throughput
* ***Latency*** is the time required to perform some action or to produce some result
  * Measured in units of time - hours, minutes, seconds, nanoseconds or clock periods
  * I/O latency: the time that it takes to complete a single I/O
* ***Throughput*** is the number of such actions executed or results produced per unit of time
  * Measureed in units of whatever is being produced (e.g., data) per unit of time
  * Disk throughput: the maximum rate of sequential data transfer, measured by Mb/sec etc.

### Moving data to workers
* In traditional cluster architectures, storage is viewed as a distinct and separate component from computation
* As dataset sizes increase, the link between the compute nodes and the storage becomes a bottleneck

### Distributed file system
* Don't move data to workers... move workers to the data
  * Store data on the local disks of nodes in the cluster
  * Start up the workers on the node that has the data local
* Why?
  * Not enough RAM to hold all the data in memory
  * Disk access is slow (low latency), but disk throughput is reasonable (high throughput)
* A distributed file system is the answer
  * A ***distrbuted file system*** is a client/server-based application that allows clients to access and process data stored on the server as if it were on their own computer
  * GFS (Google File System) for Google's MapReduce
  HDFS (Hadoop Distributed File System) for Hadoop

### Assumptions and goals of HDFS
* Very large datasets
  * 10K nodes, 100 million files, 10PB
* Streaming data access
  * Designed more for batch processing rather than interactive use by users
  * The emphasis is on hgih throughput of data access rather than low latency of data access
* Simple coherency model
  * Built around the idea that the most efficient data processing pattern is a write-once read-many-times pattern
  * A file once created, written, and closed need not be changed except for appends and truncates
* "Moving comptation is cheaper than moving data"
  * Data locations exposed so that computations can move to where data resides
* Assumes commodity hardware
  * Files are replicated to handle hardware failure
  * Hardware failure is normal rather than exception. Detect failures and recover from them
* Portability across heterogeneous hardware and software platforms
  * Designed to be eaily portable from one platform to another
* HDFS is **NOT** suited for:
  * Low-latency data access (HBase is a better option)
  * Lots of small files (NameNodes hold metadata in memory)

### HDFS Architecture
* HDFS is a block-structured file system: files broken into blocks of 64MB or 128MB
* A file can be made of several blocks, and they are stored across a cluster of one or more machines with data storage capacity
* Each block of a file is replicated across a number of machines to prevent loss of data
* HDFS has a master/slave architecture
* There are two types (and a half) of machines in a HDFS cluster
  * ***NameNode***: the heart of a HDFS, it maintains and manages the file system metadata e.g., what blocks make up a file and on which datanodes those blocks are stored
    * Only one in a HDFS cluster
  * ***DataNode***: whwere HDFS stores the actual data, serves read, write requests, performs block creation, deletion and replication upon instruction from NameNode
    * A number of DataNodes usually one per node in a cluster
    A file is split into one or more blocks and set of blocks are stored in DataNodes
  * ***SecondaryNameNode***: **NOT** a backup of NameNode
    * Checkpoint node. Periodic merge of transaction log
    * Help NameNode start up faster next time

### Functions of a NameNode
* Managing the file system namespace:
  * Maintain the namespace tree operations like opening, closing and renaming files and directories
  * Determine the mapping of file blocks to DataNodes (the physical location of file data)
  * Store file metadata
* Coordinating file operations
  * Directs clients to DataNodes for reads and writes
  * No data is moved through the NameNode
* Maintaining overall health:
  * Collect block reports and heartbeats from DataNodes
  * Block re-replication and rebalancing
  * Garbage collection

NameNode Metadata
* HDFS keeps the entire namespace in RAM, allowing fast access to the metadata (4GB of local RAM is sufficient)
* Types of metadata
  * List of files
  * List of blocks for each file
  * List of DataNodes for each block
  * File attributes e.g. creation time, replication factor
* A transaction log  (EditLog)
  * Records file creations, file deletions etc.

Inside NameNode
* FsImage - the snapshot of the filesystem when NameNode started
  * A master copy of the metadata for the file system
* EditLogs - the sequence fo changes made to teh filesytem after NameNode started
* Only in the restart of NameNode, EditLogs are applied to FsImage to get the latest snapshot of the file system
* But NameNode restart are rare in production clusters which means EditLogs can grow very large for the clusters where NameNode runs for a long period of time
  * EditLog becomes very large which will be challenging to manage
  * NameNode restart takes a long time because lot fo changes has to be merged
  * In the case of crash, we will lose huge amount of metadata since FsImage is very old
* These issues can be overcome with [Secondary NameNode](#secondary-namenode)

### Functions of DataNodes
* Responsible for serving read and write requests from the file system's clients
* Perform block creation, deletion, and replication upon instruction from the NameNode
* Periodically sends a report of all existing blocks to the NameNode (Blockreport)
* Facilitates pipelining of data -> forwards data to other specified DataNodes

### Communciation between NameNode and DataNode
* ***Heartbeats***
  * DataNodes send heartbeats to the NameNode to confirm that the DataNode is operating the block replicas it hosts are available
    * Once every 3 seconds
  * The NameNode marks DataNodes without recent Heartbeats as dead and does not forward any new IO requests to them
* ***Blockreports***
  * A Blockreport contains a list of all blocks on a DataNode
  * Every 10th heartbeat is a Blockreport
* The NameNode receives a Heartbeat and a Blockreport from each DataNode in the cluster periodically
* NameNode builds metadata from Blockreports
* If NameNode is down, HDFS is down

### Secondary NameNode
* Secondary NameNode helps to overcome the above issues by taking over reponsibility of merging EditLogs with FsImage from the NameNode
  * It gets the EditLogs from the NameNode periodically and applies to FsImage
  * Once it has new FsImage, it copies back to NameNode
  * NameNode will use this FsImage for the next restart, which will reduce the startup time

### File system namespace
* Hierarchical file system with directories and files
* Create, remove, move, rename etc.
* NameNode maintains the file system
* Any meta information changes to the file system recorded by the NameNode (EditLog)
* An application can specify the number of replicas of the file needed: replication factor of the file

### HDFS commands
* All HDFS commands are invoked by the `bin/hdfs` script. Running the hdfs script without any arguments prints the description for all commands
* Usage `hdfs [SHELL_OPTIONS] COMMAND [GENERIC_OPTIONS] [COMMAND_OPTIONS]`
  * `hdfs dfs [COMMAND [COMMAND OPTIONS]]`
  * Run a filesystem command on the file system supported in Hadoop

### Replication engine
* NameNode detects DataNode failures
  * Missing Heartbeats signify lost Nodes
  * NameNode consults metadata, finds affected data
  * Chooses new DataNodes for new replicas
  * Balances disk usage
  * Balances communication traffic to DataNodes

### Cluster rebalancing
* Goal: % disk full on DataNodes should be similar
  * Usually run when new DataNodes are added
  * Rebalancer is throttled to avoid network congestion
  * Does not interfere with MapReduce or HDFS
  * Command line tool

### Fault tolerance
* Failure is the norm rather than exception
* A HDFS instance may consist of thousands of server machines, each storing part of the file system's data
* Since we have huge number of components, and that each component has non-trivial probability of failure means that there is always some component that is non-functional
* Detection of faults and quick, automatic recovery from them is a core architecctural goal of HDFS

### Metadata disk failure
* FsImage and EditLog are central data structures of HDFS. A corruption of these files can cause a HDFS instance to be non-functional
  * A NameNode can be configured to maintain multiple copies of FsImage and EditLog
  * Multiple copies of the FsImage and EditLog files ar updated synchronously

### HDFS erasure coding
* Replication is expensive - the default 3x replication scheme in HDFS has 200% overhead in storage space and other resources
* Therefore, a natural improvement is to use Erasure Coding (EC) in place of replication, which provides the same level of fault-tolerance with much less storage space
  * Erasure Coding transforms a message of `k` symbols into a longer message with symbols such that the orginal message can be recovered from a subset of the `n` symbols
  * In typical Erasure Coding (EC) setups, the storage overhead is no more than 50%

### Unique features of HDFS
* HDFS has a bunch of unique features that make it ideal for distributed systems:
  * Failure tolerant - data is duplicated across multiple DataNodes to protect against machine failures. The default is a replication factor of 3 (every block is stored on three machines)
  * Scalability - data transfers happen directly with the DataNodes so your read/write capacity scales fairly well with the number of DataNodes
  * Space - need more disk space? Just add more DataNodes and re-balance 
  * Industry standard - other distributed applications are built on top of HDFS (HBase, MapReduce)
* HDFS is designed to process large data sets with write-one-read-many semantics, it is not for low latency access

## YARN
### Why YARN
* In Hadoop v1, MapReduce performed both processing and resource management functions
  * It consisted of a Job Tracker which was the single master. The Job Tracker allocated the resources, performed scheduling adn monitored the processing jobs
  * It assigned the map and reduce tasks on a number of subordinate processes called teh Task Trackers. The Task Trackers periodically reported their progress to the Job Tracker

### What is YARN
* YARN - “Yet Another Resource Negotiator”
  * The resource management layer of Hadoop, introduced in Hadoop 2.x
  * Monitors and manages workloads, maintains a multi-tenant environment, manages the high availability features of Hadoop, and implements security controls
* Motivation:
  * Flexibility - Enabling data processing model more than MapReduce
  * Efficiency - Improving performance and QoS
  * Resource Sharing - Multiple workloads in cluster
* YARN was introduced in Hadoop version 2.0 in the year 2012 by Yahoo and Hortonworks
* The basic idea behind YARN is to relieve MapReduce by taking over the responsibility of Resource Management and Job Scheduling
* YARN enabled the users to perform operations as per requirement by using a variety of tools like Spark for real-time processing, Hive for SQL, HBase for NoSQL and others

### YARN components
* ResourceManager
  * Arbitrates resources among all the applications in the system 
* ApplicationMaster
  * A framework specific library and is tasked with negotiating resources from the ResourceManager and working with the NodeManager(s) to execute and monitor the tasks
* NodeManager
  * The per-machine framework agent who is responsible for containers, monitoring their resource usage (cpu, memory, disk, network) and reporting the same to the ResourceManager
* Container
  * Unit of allocation incorporating resource elements such as memory, cpu, disk, network etc, to execute a specific task of the application
