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
8. [Validation](#validation)

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

The project is able to cover so much of its domain space thanks to the usage of the technique known as Randomized Testing, which is integrated via the [carrotsearch framework](https://github.com/randomizedtesting/randomizedtesting). This approach allows the developers to greatly vary the input data, both in content and volume, between runs of the suite. In addition, through the use of [Puppet](https://puppetlabs.com/), the runtime environment itself is randomized, be it through the variation in factors such as the version of the JVM used and the operating system, this even includes running different versions of Elasticsearch in the same cluster during a single test. This supplements the unit tests in catching bugs that break previously working functionality, that is, it functions as regression testing. It also assures that new versions remain backwards compatible with older ones. Random tests that fail output the seed that was used to generate them so they can be rerun in the future.

<a name="controllability" />
Controllability
---------------
When it comes to the Elasticsearch code itself, the developers have enough flexibility to change input parameters as is necessary for any given test. However, external factors such as connection speeds and network congestion remain difficult to account for. However in classes such as (MockServiceTransport)[https://github.com/elastic/elasticsearch/blob/b6c21cc55ab4167a367d1a3c812e3b3659e3dcb9/test-framework/src/main/java/org/elasticsearch/test/transport/MockTransportService.java], these conditions can be simulated.

<a name="observability" />
Observability
-------------
In the case of end-to-end testing, done on the REST API level, tests amount to sending a JSON-encoded request to the system and comparing the also-JSON-encoded response to the expected result, according to the [specification](https://github.com/elastic/elasticsearch/tree/master/rest-api-spec). In the case of the Java Unit tests, the internal state of the various objects can be inspected.

<a name="isolateability" />
Isolateability
--------------
In addition to unit testing of already isolated components, Elasticsearch's testing suite features various mock objects that allow for the minimization of the effect of other code in the test.

<a name="separation_of_concerns" />
Separation of concerns
----------------------
Functionality is duly separated in classes and methods, as such, tests that validate a certain functionality nedd only target those classes and methods that implement them.

<a name="understandability" />
Understandability
-----------------
The modules composing Elasticsearch are detailed in the [documentation](https://www.elastic.co/guide/en/elasticsearch/reference/current/modules.html). In addition, each package, class and method is aptly named according to its designated function, as well as occasionally commented. As such, the role of each component can be adequately derived.

<a name="heterogeneity" />
Heterogeneity
-------------
The differences inherent in Java interfaces and the REST API, means that the testing to the latter has to be done differently from the rest of the codebase which is tested using JUnit/carrotsearch. In the REST API tests a JSON request is sent to the system, and the reply, also in JSON is validated against the expected results. In the other tests, Java methods are invoked and their return values as well the attributes of the various classes are checked.

<a name="statistics" />
Statistics
----------
[Unit Tests](http://people.apache.org/~rmuir/es-coverage/unit-tests/)
[Integration Tests](http://people.apache.org/~rmuir/es-coverage/integ-tests/)
[Combined](http://people.apache.org/~rmuir/es-coverage/combined/)
[Jenkins](http://build-us-00.elastic.co/)
TODO: replace with originals

<a name="validation" />
Validation
----------
Elasticsearch's community is very keen on giving feedback to various existent blogs created by users themselves as well as participating in conferences with the  

Elasticsearch counts on its avid community to point to problems to [their approach](https://aphyr.com/posts/317-call-me-maybe-elasticsearch), pushing the 




