Storm Maven Plugin
===================

The intent of Storm Maven Plugin project is to create a Maven 2.x.x/3.x.x-compatible plugin that facillitates the creation, deployment, and undeployment of Storm topologies as easily as possible from a Maven-based build/continuous integration environment.

The plugin will rely as much as possible on project (POM) properties to operate, in order to minimize plugin-specific configuration requirements. For example, the name of the storm .jar file to submit to a topology can be inferred based on the maven POM, and need not be specified in the configuration.   
   
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
      
Status
------
This project is currently under active development in a "Proof of Concept" phase. Source code should be posted soon.

To contribute code, feature requests, suggestions, etc., use GitHub's pull request, issue management, and gist features, or contact the author (ptgoetz).

   
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
      
Maven Goals
-----------

Initially, the plugin will aim provide the following goals:

**`storm:package`**

* create a storm topology jar file, ready for deployment to a storm cluster

**`storm:jar`**

* submit a topology to a cluster (running the "storm:package" goal first, if necessary)
* equivalent to running the "storm jar" command.


**`storm:kill`**

* shutdown a topology on a storm cluster
* equivalent to running the "storm kill" command

**`storm:swap`**

* update a running topology (running the "storm:package" goal first, if necessary)
* equivalent to running the "storm swap" command

**`storm:run`**

* run a topology in local mode (within the Maven JVM context)

For more information on command-line equivalents of the maven goals see 
[Running Topologies on a Production Cluster](https://github.com/nathanmarz/storm/wiki/Running-topologies-on-a-production-cluster)
   
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
   
Plugin Configuration
-------------

**`stormHome`**

* The path to the local Storm installation
* Command line override: `-Dmaven.storm.home=<value>`

**`topologyClass`**

* The class name of the topology driver (e.g. "com.foo.bar.MyTopology")
* Command line override: `-Dmaven.storm.topology=<value>`

**`nimbusHost`**

* The hostname of the cluster's Nimbus node
* Command line override: `-Dmaven.storm.nimbus.host=<value>`

**`args`**

* A list of arguments to be passed to the main() method of the topology class.
* Command line override: `-Dmaven.storm.args.0=foo -Dmaven.storm.args.1=bar`
   
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
   
Example Configuration
---------------------

			<plugin>
				<groupId>com.instanceone.storm</groupId>
				<artifactId>storm-maven-plugin</artifactId>
				<version>0.0.1-SNAPSHOT</version>
				<configuration>
					<stormHome>/Users/tgoetz/java/storm-0.5.4</stormHome>
					<topologyClass>com.foo.bar.MyTopology</topologyClass>
					<nimbusHost>master</nimbusHost>
					<args>
						<arg>foo</arg>
						<arg>bar</arg>
					</args>
				</configuration>
			</plugin>