# BIRT Runtime Bundle

This module provides all necessary dependencies to run a BIRT engine in your Java application.

All dependencies declared in the [pom.xml](pom.xml) file will be transitively available to projects that include `birt-runtime-bundle` as a dependency:


**Gradle**

    compile (group: 'ch.reportingsoft.birt', name: 'birt-runtime-bundle', version: '1.18.0', changing: true)

**Maven**

    <dependency>
        <groupId>ch.reportingsoft.birt</groupId>
        <name>birt-runtime-bundle</name>
        <version>1.18.0</version>
        <type>pom</type>
    </dependency>


    

