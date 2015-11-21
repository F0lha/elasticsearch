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
Distributed systems, by their very nature, present numerous and difficult testing and deployment challenges, as they need to be operational in a myriad, sometimes unstable production environments. Different operating systems and runtime environments between servers, variable connection speeds and network throughput, timing and communication requirements, and node failures and congestion are but some of the problems that must be accounted for in verifying that the system works properly. 

As such, it becomes necessary to test at the per-commit basis, so as to catch each bug that is introduced as soon as possible, with as many configurations and scenarios as is feasible. In addition to encouraging each contributor to test their changes locally, the core team behind Elasticsearch continuously runs its suite of tests using the tool [Jenkins](https://jenkins-ci.org/). This tool currently hosts [multiple tests](http://jenkins.elasticsearch.org/) running in parallel.
=======
As such, it becomes necessary to test at the per-commit basis, so as to catch each bug that is introduced as soon as possible, with as many configurations and scenarios as is feasible. In addition to encouraging each contributor to test their changes locally, the core team behind Elasticsearch continuously runs its suite of tests using the tool [Jenkins](https://jenkins-ci.org/). This tools currently hosts [multiple tests](http://jenkins.elasticsearch.org/) running in parallel of different versions of the software.
>>>>>>> origin/master

The testing suite is divided into four main categories:
  - Smoke-test: The first and most straight-forward test is to verify that the committed code compiles at all. Needless to say this constitutes a precondition for the following tests.
  - Unit Test: Individual components and class methods are tested in isolation to validate their functionality.
  - Integration Tests: Takes modules that have been Unit tested, groups them in larger aggregates and applies tests. These aim at catching problems in the interfacing or coupling of different components. 
  - End-to-end Tests: Finally, the entire system is checked as a whole and compared to its expected functionality. In Elasticsearch in particular, this entails sending REST requests and queries to the system and validating its JSON responses, with the aid of the [API specification](https://github.com/F0lha/elasticsearch/tree/master/rest-api-spec). These tests are currently written declaratively in [YAML](http://yaml.org/) format.

The project is able to cover so much of its domain space thanks to the usage of the technique known as Randomized Testing, which is integrated via the [carrotsearch framework](https://github.com/randomizedtesting/randomizedtesting). This approach allows the developers to greatly and randomly vary the input data, both in content and volume, between runs of the tests. In addition, through the use of [Puppet](https://puppetlabs.com/), the runtime environment itself can be randomized, be it through the variation in factors such as the version of the JVM and operating system used, or through the variation in the versions of Elasticsearch used in the same cluster during a single test. This supplements the unit tests in catching bugs that break previously working functionality, that is, it serves as regression testing. It also assures that new versions remain backwards compatible with older ones and that they remain capable of talking to eachother. Prior to each random run, the seed that is used to generate them is output so as to facilitate its reproduction in the future. This is especially important for tests that end up failing as any supposed fixes to the problem(s) that made them fail can be verified by running the tests with that same seed. Over time, a repertoire of potentially problematic seeds is accumulated and used in each subsequent run, further increasing the reliability of the testing process in detecting erroneous behaviour.

<a name="controllability" />
Controllability
---------------
When it comes to the Elasticsearch code itself, the developers have enough flexibility to change input parameters as is necessary for any given test. In constrast, external factors such as connection speeds and network congestion remain difficult to account for. However in classes such as [MockServiceTransport](https://github.com/elastic/elasticsearch/blob/b6c21cc55ab4167a367d1a3c812e3b3659e3dcb9/test-framework/src/main/java/org/elasticsearch/test/transport/MockTransportService.java), these conditions can be simulated, although the testing environment can never truly be made the same as a deployment environment. In addition, its many external dependencies such as Lucene, Netty, Guava present a further point of weakness in the testing as their behaviour and state cannot be directly manipulated; their interfaces must instead be used (much like a black box). The rest of the code is tested with the knowledge of its implementation and thus constituting white-box testing.

<a name="observability" />
Observability
-------------
In the case of end-to-end testing, done on the REST API level, tests amount to sending a JSON-encoded request to the system and comparing the also-JSON-encoded response to the expected result, according to the [specification](https://github.com/elastic/elasticsearch/tree/master/rest-api-spec). In the case of the Java Unit tests, the internal state of the various objects can be inspected. The result of the tests is [displayed in the command line](http://build-us-00.elastic.co/job/elastic,painless,master/lastBuild/console).

<a name="isolateability" />
Isolateability
--------------
In addition to unit testing of already isolated components, Elasticsearch's testing suite features various mock objects that allow for the minimization of the effect of other code in the test.

<a name="separation_of_concerns" />
Separation of concerns
----------------------
Functionality is duly separated in classes and methods, as such, tests that verify a certain functionality need only target those classes and methods that implement them.

<a name="understandability" />
Understandability
-----------------
The modules composing Elasticsearch are detailed in the [documentation](https://www.elastic.co/guide/en/elasticsearch/reference/current/modules.html). In addition, each package, class and method is aptly named according to its designated function, as well as occasionally commented. As such, the role of each component can be adequately derived.

<a name="heterogeneity" />
Heterogeneity
-------------
The differences inherent in Java interfaces and the REST API mean that the testing to the latter has to be done differently from the rest of the codebase which is tested using JUnit/carrotsearch. In the REST API tests, a JSON request is sent to the system, and the reply, also in JSON, is compared with the expected results. In the other tests, Java methods are invoked and their return values as well the attributes of the various classes are checked.

<a name="statistics" />
Statistics
----------
[Unit Tests](http://people.apache.org/~rmuir/es-coverage/unit-tests/)
[Integration Tests](http://people.apache.org/~rmuir/es-coverage/integ-tests/)
[Combined](http://people.apache.org/~rmuir/es-coverage/combined/)
[Jenkins](http://build-us-00.elastic.co/)

<a name="validation" />
Validation
----------
The stakeholders, the ones that utilize Elasticsearch, are, in turn, developers themselves, who have chosen it as their search solution over the competition, which includes projects such as [Solr](http://lucene.apache.org/solr/) via acceptance testing, that is, each developer assesses the system and its features against their particular use case. 

As is expected from such a knowledgeable and invested userbase, feedback about the status of the project is enormous and typically [comprehensive](https://aphyr.com/posts/317-call-me-maybe-elasticsearch). It can be found on the [Elasticsearch forums](https://discuss.elastic.co/c/elasticsearch), in the [issues section on GitHub](https://github.com/elastic/elasticsearch/issues?utf8=%E2%9C%93&q=) and in various [blogs](http://blog.quarkslab.com/mongodb-vs-elasticsearch-the-quest-of-the-holy-performances.html) and [videos](https://www.elastic.co/videos/just-eat-journey-nosql-elasticsearch) on the Internet. 
The core team is [always](https://github.com/elastic/elasticsearch/issues/14573) receptive to this feedback, going as far as releasing beta and release candidate versions specifically for the purpose of gathering the communities reactions and criticism, in addition to the already frequent release schedule. 
