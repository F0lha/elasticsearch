ESOF - Third Report
====================
Elasticsearch is a distributed search engine and data storage system based on Apache Lucene.

<a name="index"/>
## Menu
1. [Introduction](#intro)
1. [Implementation View](#implementation)
2. [Logical View](#logical)
3. [Process View](#process)
4. [Deployment View](#deployment)
5. [Architectural Patterns](#patterns)

<a name="intro" />
Introduction
------------
The purpose of this report is to better explain some of the attributes of Elasticsearch. Using the 4+1 Architectural View Model, whose diagrams can be seen below, it is much easier to comprehend Elasticsearch's arquitectural aspects.

Firstly, some of the terms used in the diagrams will be explained for a better understanding of the matter.

Then, the diagrams of the 4+1 Architectural View Model as well as its explanations will be presented. Starting with the Component Diagram, referent to the Implementation View, followed by the Package Diagram, referent to the Logical View, Activity Diagram is next, referent to the Process View and finally the Deployment Diagram, referent to the Deployment View. These four views represent the 4 in the architectural view model mentioned before. As for the +1, it stand for the Use Cases Model which was presented in the last report.

<a name="implementation" />
Implementation View
-------------------
<p align="center">
  <img src="images/component.PNG" >
    <span class="caption">
      <p align="center">Component Diagram</p>
    </span>
</p>
<a name="logical"/>
Logical View
------------
<p align="center">
  <img src="images/package.png" >
    <span class="caption">
      <p align="center">Package Diagram</p>
    </span>
</p>
<a name="process"/>
Process View
------------
<p align="center">
  <img src="images/process.PNG" >
    <span class="caption">
      <p align="center">Activity Diagram</p>
    </span>
</p>
<a name="deployment"/>
Deployment view
---------------
<p align="center">
  <img src="images/deployment.PNG">
  <span class="caption">
      <p align="center">Deployment Diagram</p>
  </span>
</p>

<a name="patterns"/>
Architectural Patterns
----------------------

* Data flow
* Client Server
