Apache Kafka
=================
See our [web site](http://kafka.apache.org) for details on the project.

You need to have [gradle](http://www.gradle.org/installation) installed.

### First bootstrap and download the wrapper ###
    cd kafka_source_dir
    gradle

Now everything else will work

### Building a jar and running it ###
    ./gradlew jar  

Follow instuctions in http://kafka.apache.org/documentation.html#quickstart

### Building source jar ###
    ./gradlew srcJar

### Building javadocs and scaladocs ###
    ./gradlew javadoc
    ./gradlew javadocJar # builds a jar from the javadocs
    ./gradlew scaladoc
    ./gradlew scaladocJar # builds a jar from the scaladocs
    ./gradlew docsJar # builds both javadoc and scaladoc jar

### Running unit tests ###
    ./gradlew test

### Forcing re-running unit tests w/o code change ###
    ./gradlew cleanTest test

### Running a particular unit test ###
    ./gradlew -Dtest.single=RequestResponseSerializationTest core:test

### Running a particular test method within a unit test ###
    ./gradlew core:test --tests kafka.api.ProducerFailureHandlingTest.testCannotSendToInternalTopic
    ./gradlew clients:test --tests org.apache.kafka.clients.MetadataTest.testMetadataUpdateWaitTime

### Running a particular unit test with log4j output ###
    change the log4j setting in either clients/src/test/resources/log4j.properties or core/src/test/resources/log4j.properties
    ./gradlew -i -Dtest.single=RequestResponseSerializationTest core:test

### Building a binary release gzipped tar ball ###
    ./gradlew clean
    ./gradlew releaseTarGz  
    The above command will fail if you haven't set up the signing key. To bypass signing the artifact, you can run
    ./gradlew releaseTarGz -x signArchives

The release file can be found inside ./core/build/distributions/.

### Cleaning the build ###
    ./gradlew clean

### Running a task on a particular version of Scala (either 2.10.6 or 2.11.7) ###
#### (If building a jar with a version other than 2.10, need to set SCALA_BINARY_VERSION variable or change it in bin/kafka-run-class.sh to run quick start.) ####
    ./gradlew -PscalaVersion=2.11.7 jar
    ./gradlew -PscalaVersion=2.11.7 test
    ./gradlew -PscalaVersion=2.11.7 releaseTarGz

### Running a task for a specific project ###
This is for 'core', 'examples' and 'clients'
    ./gradlew core:jar
    ./gradlew core:test

### Listing all gradle tasks ###
    ./gradlew tasks

### Building IDE project ####
    ./gradlew eclipse
    ./gradlew idea

### Building the jar for all scala versions and for all projects ###
    ./gradlew jarAll

### Running unit tests for all scala versions and for all projects ###
    ./gradlew testAll

### Building a binary release gzipped tar ball for all scala versions ###
    ./gradlew releaseTarGzAll

### Publishing the jar for all version of Scala and for all projects to maven ###
    ./gradlew uploadArchivesAll

Please note for this to work you should create/update `~/.gradle/gradle.properties` and assign the following variables

    mavenUrl=
    mavenUsername=
    mavenPassword=
    signing.keyId=
    signing.password=
    signing.secretKeyRingFile=

### Publishing the jars without signing to a local repository ###
    ./gradlew -Dorg.gradle.project.skipSigning=true -Dorg.gradle.project.mavenUrl=file://path/to/repo uploadArchivesAll

### Building the test jar ###
    ./gradlew testJar

### Determining how transitive dependencies are added ###
    ./gradlew core:dependencies --configuration runtime
	
### Running checkstyle on the java code ###
    ./gradlew checkstyleMain checkstyleTest

### Limit the number of processes for each task ###
    ./gradlew -Dorg.gradle.project.maxParallelForks=1 test

This will most commonly be useful for automated builds where the full resources of the host running the build and tests
may not be dedicated to Kafka's build.

### Running in Vagrant ###

See [vagrant/README.md](vagrant/README.md).

### Contribution ###

Apache Kafka is interested in building the community; we would welcome any thoughts or [patches](https://issues.apache.org/jira/browse/KAFKA). You can reach us [on the Apache mailing lists](http://kafka.apache.org/contact.html).

To contribute follow the instructions here:
 * http://kafka.apache.org/contributing.html

We also welcome patches for the website and documentation which can be found here:
 * https://svn.apache.org/repos/asf/kafka/site
