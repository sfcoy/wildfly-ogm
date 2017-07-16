# WildFly with Hibernate OGM + Search

This Dockerfile builds a WildFly image that includes support for Hibernate OGM using modules as described in
[How to package Hibernate OGM applications for WildFly 10](https://docs.jboss.org/hibernate/stable/ogm/reference/en-US/html_single/?v=5.1#ogm-configuration-jbossmodule).

It includes compatible upgraded versions of 

 * Hibernate ORM
 * Hibernate Search
   
   
## Build the image

    docker build --tag sfcoy/wildfly-ogm .

## Faster repeated builds

If you're using a repository manager such as [Sonatype Nexus](https://www.sonatype.com/nexus-repository-sonatype)
then you can speed up repeated builds by using Maven to pre-fetch the hibernate-orm-modules, hibernate-search-modules
 and  hibernate-ogm-modules.
 
This will then make the packaged modules available locally for download:

    mvn dependency:get -Dartifact=org.hibernate:hibernate-orm-modules:5.1.8.Final:zip:wildfly-10-dist
    mvn dependency:get -Dartifact=org.hibernate.ogm:hibernate-ogm-modules:5.1.0.Final:zip:wildfly-10-dist
    mvn dependency:get -Dartifact=org.hibernate:hibernate-search-modules:5.6.1.Final:zip:wildfly-10-dist

You can then build the image with (for example):

    docker build --tag sfcoy/wildfly-ogm --build-arg MAVEN_REPO=http://newhope.resolvesw.com.au:8081/nexus/content/groups/public/ .
    
