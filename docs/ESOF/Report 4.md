ESOF - Fourth Report
====================
Elasticsearch is a distributed search engine and data storage system based on Apache Lucene.

<a name="index"/>
## Menu
1. [Introduction](#intro)
2. [Controllability](#controllability)
3. [Observability](#observability)
4. [Isolateability](#isolateability)
5. [Separation of concerns](#separation_of_concerns)
6. [Understandability](#understandability)
7. [Heterogeneity](#heterogeneity)

<a name="intro" />
Introduction
------------
Distributed systems, by their very nature, present numerous and difficult testing and deployment challenges, as they need to be operational in a myriad, sometimes unstable production environments. Different operating systems and runtime environments between servers, variable connection speeds and network throughput, timing and communication requirements, and node failures and congestion are but some of the problems that must be accounted for in verifying and validating the system. *TODO: add stuff*

As such, it becomes necessary to test at the per-commit basis, so as to catch each bug that is introduced as soon as possible, with as many configurations and scenarios as is feasible. *TODO: add stuff*

The core team behind Elasticsearch continuously runs its suite of tests using the tool [Jenkins](https://jenkins-ci.org/) *TODO: add stuff*

The testing suite is divided into four main categories:
  - Smoke-test: The first and most straight-forward test is to verify that the committed code compiles
  - Unit Test: Individual components and class methods are tested in isolation to validate their functionality
  - Integration Tests: These aim at catching problems in the interfacing or coupling of different components *TODO add stuff*
  - End-to-end Tests: Finally, the entire system is checked as a whole and compared to its expected functionality. In Elasticsearch in particular, this entails sending REST requests and queries to the system and validating its JSON responses, with the aid of the [API specification](https://github.com/F0lha/elasticsearch/tree/master/rest-api-spec). This is currently done in YAML format. *TODO change stuff* 

The project is able to cover so much of its domain space thanks to the usage of the technique known as Randomized Testing, which is integrated via the [carrotsearch framework](https://github.com/randomizedtesting/randomizedtesting). This approach allows the developers to greatly vary the input data, both in content and volume, between runs of the suite. In addition, through the use of [Puppet](https://puppetlabs.com/), the runtime environment itself is randomized, be it through the variation in factors such as the version of the JVM used and the operating system, this even includes running different versions of Elasticsearch in the same cluster during a single test. This supplements the unit tests in catching bugs that break previously working functionality, that is, it functions as regression testing. It also assures that new versions remain backwards compatible with older ones.

<a name="controllability" />
Controllability
---------------

<a name="observability" />
Observability
-------------

<a name="isolateability" />
Isolateability
--------------

<a name="separation_of_concerns" />
Separation of concerns
----------------------

<a name="understandability" />
Understandability
-----------------

<a name="heterogeneity" />
Heterogeneity
-------------

<a name="statistics" />
Statistics
----------

[Unit Tests](http://people.apache.org/~rmuir/es-coverage/unit-tests/)
[Integration Tests](http://people.apache.org/~rmuir/es-coverage/integ-tests/)
[Combined](http://people.apache.org/~rmuir/es-coverage/combined/)
[Jenkins](http://build-us-00.elastic.co/)
TODO: replace with originals

