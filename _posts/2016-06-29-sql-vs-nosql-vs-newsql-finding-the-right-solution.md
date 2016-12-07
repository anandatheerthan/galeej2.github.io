---
layout: post
title: SQL VS. NOSQL VS. NEWSQL: FINDING THE RIGHT SOLUTION
date: 2016-06-29 07:25
author: administrator
comments: true
categories: [Reference]
---
If you are happy with the performance, scalability, and high availability of your current traditional SQL database system (the likes of Oracle, SQL Server, MySQL), then there is no reason to read further. However, if you have growing pains in any of these areas, then a NoSQL or NewSQL offering may be right for you. So how do you choose between them?

Choosing the right tool for the job at hand is 80% of getting to a solution; the other 20% is really understanding the problem you’re trying to solve. Here’s a rundown of the advantages and disadvantages of traditional SQL databases (affectionately called OldSQL in this article), NoSQL and NewSQL that can help you focus your data store choices.
<h3><strong>OLDSQL</strong></h3>
Traditional SQL databases have been around for decades and serve as the core foundation of nearly every application we use today. If you have a deployed application and it is behaving and performing acceptably, that is fantastic; there is no need to change your data store. Realize that porting or replacing your database not only introduces work, it introduces risk. It is rare that a database replacement candidate is feature-for-feature, as well as bug-for-bug, compatible with the database you are replacing. Beware any vendor who suggests otherwise! Here are some of the typical patterns of a traditional database application:
<h4><strong>THE OLDSQL ADVANTAGES:</strong></h4>
<ul>
 	<li>Proven disk-based database technology and standard SQL support, hardened over several decades.</li>
 	<li>Compatible with ORM layers, such as Hibernate or ActiveRecord.</li>
 	<li>Rich client-side transactions.</li>
 	<li>Ad hoc query and reporting.</li>
 	<li>An established market and ecosystem with vast amounts of standards-based tooling.</li>
</ul>
<h4><strong>THE OLDSQL DISADVANTAGES:</strong></h4>
<ul>
 	<li>Not a scale-out architecture. Transactional throughput is often gated by the capacity of a single machine. Scaling out requires application-defined and managed sharding (or partitioning) of the data.</li>
 	<li>Traditional SQL systems were built for “one size fits all.” They are good for general purpose applications with modest performance requirements, but struggle as needs grow.</li>
 	<li>Complex tuning parameters often require deep expertise to get the best balance between performance, data safety, and resource use.</li>
</ul>
<h3><strong>NOSQL</strong></h3>
First, realize that the term NoSQL is about as descriptive as categorizing dogs and horses as “NoCats”. In truth, NoSQL is a broad category collecting disparate technologies beneath an ambiguous umbrella. The term offers little help to the developer trying to decide on the right tool for the right job.

So let’s break it down with an eye on what we really care about as software engineers: what problems can I solve with NoSQL? Equally important, where is NoSQL a bad fit? Where do the different technologies show their strengths?
<h4><strong>SOME NOSQL SYSTEMS PUT AVAILABILITY FIRST</strong></h4>
Say you have gigabytes to petabytes of data. New data is added regularly and, once added, is relatively static. A database that archives sensor readings or ad impression displays is a good example. You want to store this in a cloud and are willing to tolerate the programming challenges of eventual consistency (made easier because most updates are idempotent anyway) for distributed access, multi-datacenter replication, and the highest possible availability.

Your application-to-database interactions are simple “CREATE” and “GET” patterns that don’t require traditional transactions. The most important consideration is that the database is always available to accept new content and can always provide content when queried, even if that content is not the most recent version written. Such systems include DynamoDB, Riak and Cassandra.
<h4><strong>SOME NOSQL SYSTEMS FOCUS ON FLEXIBILITY</strong></h4>
Made famous by MongoDB and CouchDB, the Document Model expands upon the traditional key-value store by replacing the values with JSON-structured documents, each able to contain sub-keys and sub-values, arrays of value, or hierarchies of all of the above. Often described as schemaless, these systems don’t enforce premeditated or consistent schema across all of the stored documents. This makes managing schema different… less rigid, but also much messier. It is likely the benefits of this approach are more applicable for smaller development teams with simpler data needs.

Other systems expand upon key-value stores with organizational features. Redis is popular for creating many sorted lists of data for easy ranking and leaderboards. By adding more complex functions to order by and computer statistics on, its focus allows for functionality key to its specific use cases.
<h4><strong>SOME NOSQL SYSTEMS FOCUS ON ALTERNATIVE DATA MODELS OR SPECIAL USE CASES</strong></h4>
The most common examples are systems tuned for graph processing, such as Neo4j. Array databases are another such example; SciDB uses Python and R to access MPP array data for scientific research. Accumulo is a variation on the wide-column-store model popularized by Cassandra and BigTable, but with a focus on cell-level security. Systems like etcd are distributed datastores with a focus on storing configuration data for other services. Elasticsearch is a popular system for implementing text search within applications.
<h4><strong>THE NOSQL ADVANTAGES:</strong></h4>
<ul>
 	<li>Eventual-consistency algorithms allow implementations to deliver the highest availability across multiple data centers.</li>
 	<li>Eventual-consistency based systems scale update workloads better than traditional
OLAP RDBMs, while also scaling to very large datasets.</li>
 	<li>Many NoSQL systems are optimized to support non-relational data, such as log messages, XML and JSON documents, as well as unstructured documents, allowing you to skip specifying schema-on-write, and allowing you to specify a schema-on-read.</li>
</ul>
<h4><strong>THE NOSQL DISADVANTAGES:</strong></h4>
<ul>
 	<li>These systems are fundamentally not transactional (ACID). If they advertise otherwise, beware the over-reaching claim.</li>
 	<li>OLAP-style queries require a lot of application code. While the write-scaling advantages are appealing vs. OLAP stores (such as Vertica or GreenPlum), you sacrifice declarative ad hoc queries – important to historical analytical exploration.</li>
</ul>
<h3><strong>NEWSQL</strong></h3>
The term NewSQL is not quite as broad as NoSQL. NewSQL systems all start with the relational data model and the SQL query language, and they all try to address some of the same sorts of scalability, inflexibility or lack-of-focus that has driven the NoSQL movement. Many offer stronger consistency guarantees.

But within this group there are many differences. HANA was created to be a business reporting powerhouse that could also handle a modest transactional workload, a perfect fit for SAP deployments. Hekaton adds sophisticated in-memory processing to the more traditional Microsoft SQL Server. Both systems are non-clustering for now, and both are designed to replace or enhance OldSQL deployments directly.

NuoDB set out to be a cluster-first SQL database with a focus on cloud-ops: run on many nodes across many datacenters and let the underlying system manage data locality and consistency for you. This comes at a cost in performance and consistency for arbitrary workloads. For workloads that are closer to key-value, global data management is a more tractable problem. NuoDB is the closest to being called eventually consistent of the NewSQL systems.

Other systems focus on clustered analytics, such as MemSQL. Distributed, with MySQL compatibility, MemSQL often offers faster OLAP analytics than all-in-one OldSQL systems, with higher concurrency and the ability to update data as it’s being analyzed.

<a href="http://voltdb.com/">VoltDB</a>, the most mature of these systems, combines streaming analytics, strong ACID guarantees and native clustering. This allows VoltDB to be the system-of-record for data-intensive applications, while offering an integrated high-throughput, low-latency ingestion engine. It’s a great choice for policy enforcement, fraud/anomaly detection, or other fast-decisioning apps.
<h4><strong>THE NEED FOR SPEED: FAST IN-MEMORY SQL</strong></h4>
Perhaps you have gigabytes to terabytes of data that needs high-speed transactional access. You have an incoming event stream (think sensors, mobile phones, network access points) and need per-event transactions to compute responses and analytics in real time. Your problem follows a pattern of “ingest, analyze, decide,” where the analytics and the decisions must be calculated per-request and not post-hoc in batch processing. NewSQL systems that offer the scale of NoSQL with stronger consistency may be the right choice.
<h4><strong>THE NEWSQL ADVANTAGES:</strong></h4>
<ul>
 	<li>Minimize application complexity stronger consistency and often full transactional support.</li>
 	<li>Familiar SQL and standard tooling.</li>
 	<li>Richer analytics leveraging SQL and extensions.</li>
 	<li>Many systems offer NoSQL-style clustering with more traditional data and query models.</li>
</ul>
<h4><strong>THE NEWSQL DISADVANTAGES:</strong></h4>
<ul>
 	<li>No NewSQL systems are as general-purpose as traditional SQL systems set out to be.</li>
 	<li>In-memory architectures may be inappropriate for volumes exceeding a few terabytes.</li>
 	<li>Offers only partial access to the rich tooling of traditional SQL systems.</li>
</ul>
<h3><strong>SUMMING IT UP</strong></h3>
As a general rule of thumb, consider evaluating NoSQL offerings if you favor availability or have special data model needs. Consider NewSQL if you’d like the at-scale speed of NoSQL, but with stronger consistency and the familiar and powerful SQL query language.

The froth in the data management space is substantial – and our tendency to talk in terms of categories (SQL, NoSQL, NewSQL) vs. problems makes it hard for software developers to understand what’s in the toolbox. The current offerings of new databases are not all alike – and recognizing how the DNA behind each helps or hinders problem solvers is the key to choosing the best solution.
