ESOF - Third Report
====================
Elasticsearch is a distributed search engine and data storage system based on Apache Lucene.

<a name="index"/>
## Menu
1. [Introduction](#intro)
2. [Lucene Library](#lucene)
3. [REST API](#rest)
4. [Implementation View](#implementation)
5. [Logical View](#logical)
6. [Process View](#process)
7. [Deployment View](#deployment)
8. [Architectural Patterns](#patterns)

<a name="intro" />
Introduction
------------
The purpose of this report is to better explain some of the attributes of Elasticsearch. Using the 4+1 Architectural View Model, whose diagrams can be seen below, it is much easier to comprehend Elasticsearch's arquitectural aspects.

Firstly, some of the terms used in the diagrams will be explained for a better understanding of the matter.

Then, the diagrams of the 4+1 Architectural View Model as well as its explanations will be presented. Starting with the Component Diagram, referent to the Implementation View, followed by the Package Diagram, referent to the Logical View, Activity Diagram is next, referent to the Process View and finally the Deployment Diagram, referent to the Deployment View. These four views represent the 4 in the architectural view model mentioned before. As for the +1, it stand for the Use Cases Model which was presented in the last report.

<a name="lucene" />
Lucene Library
--------------
Apache LuceneTM is a high-performance, full-featured text search engine library written entirely in Java. It is a technology suitable for nearly any application that requires full-text search, especially cross-platform.
Elasticsearch uses Lucene as a search server.

<a name="rest" />
REST API
--------
REST (REpresentational State Transfer) is an architectural style, and an approach to communications that is often used in the development of Web services.
REST'S decoupled architecture, and lighter weight communications between producer and consumer, make REST a popular building style for cloud-based APIs. When Web services use REST architecture, they are called RESTful APIs (Application Programming Interfaces) or REST APIs. Elasticsearch is a RESTful API.

<a name="implementation" />
Implementation View
-------------------
The Implementation View illustrates a system from a programmer's perspective and is concerned with software management. It uses the UML Component Diagram to describe the system components.

A Component Diagram shows how components are wired together in the software. Components are wired together by using an assembly connector to connect the required interface of one component with the provided interface of another component. This illustrates the service consumer - service provider relationship between the two components.
The Component Diagram below represents the Implementation View of Elasticsearch: 
<p align="center">
  <img src="images/component.PNG" >
    <span class="caption">
      <p align="center">Component Diagram</p>
    </span>
</p>
<a name="logical"/>
Logical View
------------
The Logical View is concerned with the functionality that the system provides to end-users. The UML Diagram used to describe this view, in this case, is the Package Diagram. 

A Package Diagram in the Unified Modeling Language depicts the dependencies between the packages that make up a model. Package diagrams can use packages that represent the different layers of a software system to illustrate the layered architecture of a software system. The dependencies between these packages can be adorned with labels/stereotypes to indicate the communication mechanism between the layers.
The Package Diagram below represents the Logical View of Elasticsearch:
<p align="center">
  <img src="images/package.png" >
    <span class="caption">
      <p align="center">Package Diagram</p>
    </span>
</p>
<a name="process"/>
Process View
------------
The Process View deals with the dynamic aspects of the system, explains the system processes and how they communicate, and focuses on the runtime behavior of the system. The Process View addresses concurrency, distribution, integrators, performance, and scalability. The UML Diagram used to represent Process View is the Activity Diagram.

Activity diagrams are graphical representations of workflows of stepwise activities and actions with support for choice, iteration and concurrency. In the Unified Modeling Language, activity diagrams are intended to model both computational and organizational processes. 
The Activity Diagram below represents the Process View of Elasticsearch:
<p align="center">
  <img src="images/process.PNG" >
    <span class="caption">
      <p align="center">Activity Diagram</p>
    </span>
</p>
<a name="deployment"/>
Deployment view
---------------
The Deployment View depicts the system from a system engineer's point of view. It is concerned with the topology of software components on the physical layer, as well as the physical connections between these components. The UML Diagram used to represent this view is the Deployment Diagram.

A Deployment Diagram in the Unified Modeling Language models the physical deployment of artifacts on nodes. The nodes appear as boxes, and the artifacts allocated to each node appear as rectangles within the boxes. Nodes may have subnodes, which appear as nested boxes. A single node in a deployment diagram may conceptually represent multiple physical nodes, such as a cluster of database servers.
The Deployment Diagram below represents the Deployment View of Elasticsearch:
<p align="center">
  <img src="images/deployment.PNG">
  <span class="caption">
      <p align="center">Deployment Diagram</p>
  </span>
</p>

<a name="patterns"/>
Architectural Patterns
----------------------
* Data flow - data is transferred throughout the system in JSON format
* Client Server - clusters and the nodes that compose them play the role of servers in the more traditional client-server architecture
