# BIRT Runtime Bundle

This module defines all the necessary dependencies to run a BIRT engine in a Java
application.

All dependencies declared in the [pom.xml](pom.xml) file will be transitively available to a
project declaring `birt-bom-runtime` in its dependencies:

Usage with Gradle:
    
    compile (group: 'ch.reportingsoft.birt', name: 'birt-runtime-bundle', version: '1.14.0', changing: true)

Usage with Maven:

    <dependency>
        <groupId>ch.reportingsoft.birt</groupId>
        <name>birt-bom-runtime</name>
        <version>1.14.0</version>
        <type>pom</type>
    </dependency>

## Launch deployment

Use the [BIRT BOM Deploy](https://lausanne.reportingsoft.ch/jenkinsnew/job/BIRT/job/BIRT%20Dependencies%20Deploy/)
Jenkins job to deploy the BOM into our Artifactory repository

    

