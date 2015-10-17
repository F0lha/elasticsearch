ESOF - Second Report
====================
Elasticsearch is a distributed search engine and data storage system based on Apache Lucene.


Functional Requirements:
* Data Storage - the system must be able to store the information to be retrieved and searched
* Distributed - storing the various documents comprising the data in multiple machines offers a wide variety of benefits, the system must be able to manage the various nodes
* Analytics - the data must be queryable for aggregations and statistics 
* Full Text Search - the ability for fuzzy/exact matching on both partial and entire data fields 
* Able to handle human language - consideration of the syntax/semantics of natural language provides more meaningful and useful results
* Able to handle geolocation data - many applications use and store geolocation data; to be able to efficiently handle it out-of-the-box is highly valued
* Highlighted Search - many applications require that the segments of the documents that matched a search be highlighted for the user
* *Search-as-you-type* functionality - interactive searches improve the end-user experience 
* *Did-you-mean* and *More-like-this* suggestions - these kinds of suggestions enable the users of an application to be redirected to other data they might be interested in
* RESTful API - a familiar and cross-language API allows for developers to quickly and easily start developing their applications
* Discovery - connected nodes should be able to automatically discover each other

Non-Functional Requirements
* High Availability - the system must endure the inevitable failures in the potentially many nodes that host the data and continue being operational
* High Throughput/Real Time Performance - fast response times and overall efficiency are highly valued, especially in highly saturated services/applications
* High Flexibility in queries/data - the schema-less, document-oriented model as well as the querying system must be flexible enough to effortlessly model any domain 
* Reliability - the data in the system must be kept through failures in the nodes that host the data
* Developer Friendliness - developers unfamiliar with distributed NoSQL systems or search engines such as Lucene must be able to quickly get up and running
* High Horizontal Scalability - the system must elegantly support the heavy load inherent in large-scale applications involving massive amounts of information

Validation of Requirements
--------------------------
Since its inception, the project has admirably met its myriad requirements, which have been repeatedly tested and verified by its many users, the principal stakeholders in the project, both in production and in its testing suite.

Its nature as a distributed search engine and data storage system requires as a main feature that the various shards that comprise the documents be distributed between various machines or nodes and that the system itself be able to appropriately manage them. Its touted high availability necessitates that the various shards be constantly communicating with each other, ready to appropriately respond to a variety of failures in the different nodes.

Both the growing need for high throughput and the need for reliability are fulfilled by the redundancy in the replicated shards housed in the nodes.

Scalable read performance is also assured by the redundancy in the data, allowing for the mass parallelization of read operations.

Scalable write performance, on the other hand, is ensured by the deployment of more machines as nodes.

Developers around the world, from any programming background, find jumping into Elasticsearch easy and manageable. Seasoned ones, on the other hand, make full use of its scalalabity and breadth, in applications both massive and small.

Use Cases
---------
![Developer Use Cases](images/use_case_1.PNG "Developer Use Cases")
![User Use Cases](images/use_case_2.PNG "User Use Cases")

Domain Model
------------
![Elasticsearch domain model](images/domain_model.PNG "Elasticsearch domain model")

Definitions, Acronyms and Abbreviations
---------------------------------------
* Cluster - A cluster consists of one or more nodes which share the same cluster name. Each cluster has a single master node which is chosen automatically by the cluster and which can be replaced if the current master node fails.

* Document - A document is a JSON document which is stored in elasticsearch. It is like a row in a table in a relational database. Each document is stored in an index and has a type and an id. A document is a JSON object which contains zero or more fields, or key-value pairs. The original JSON document that is indexed will be stored in the _source field, which is returned by default when getting or searching for a document.

* Node - A node is a running instance of elasticsearch which belongs to a cluster. Multiple nodes can be started on a single server for testing purposes, but usually there should be one node per server. At startup, a node will use unicast (or multicast, if specified) to discover an existing cluster with the same cluster name and will try to join that cluster.

* Primary Shard - Each document is stored in a single primary shard. When you index a document, it is indexed first on the primary shard, then on all replicas of the primary shard. By default, an index has 5 primary shards. You can specify fewer or more primary shards to scale the number of documents that your index can handle. You cannot change the number of primary shards in an index, once the index is created.

* Replica Shard - Each primary shard can have zero or more replicas. A replica is a copy of the primary shard, and has two purposes:
				1. increase failover: a replica shard can be promoted to a primary shard if the primary fails
				2. increase performance: get and search requests can be handled by primary or replica shards. By default, each primary shard has one replica, but the number of replicas can be changed dynamically on an existing index. A replica shard will never be started on the same node as its primary shard. 

* Shard - A shard is a single Lucene instance. It is a low-level “worker” unit which is managed automatically by elasticsearch. An index is a logical namespace which points to primary and replica shards. Other than defining the number of primary and replica shards that an index should have, it is never needed to refer to shards directly. Instead, the code should deal only with an index. Elasticsearch distributes shards amongst all nodes in the cluster, and can move shards automatically from one node to another in the case of node failure, or the addition of new nodes.


Sources
-------
* https://www.elastic.co/guide/en/elasticsearch/reference/current/glossary.html
