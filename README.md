# BIRT Runtime Bundle

This repository manages the generation and publication of BIRT Runtime libraries.

## Import the Bundle in your project

The [birt-runtime](birt-runtime) module provides all necessary dependencies
to run a BIRT engine in your Java application.

All dependencies declared in the [pom.xml](birt-runtime/pom.xml) file will be transitively available to projects that include `birt-runtime-bundle` as a dependency:


**Gradle**

    compile (group: 'ch.reportingsoft.birt', name: 'birt-runtime-bundle', version: '1.18.0', changing: true)

**Maven**

    <dependency>
        <groupId>ch.reportingsoft.birt</groupId>
        <name>birt-runtime-bundle</name>
        <version>4.18.0</version>
        <type>pom</type>
    </dependency>

# BIRT Packages Publication

### Downloading BIRT Packages

To download the required BIRT packages:

1. Navigate to the `[download-birt-package](download-birt-package)` module.
2. Run the following Maven command:
   ```bash
   mvn clean package -Pdownload-package
   ```
This command will:
- Download the BIRT public package
- Download the additional DTP (Data Tools Platform) package
- Unpack both packages into the `target` directory

### Configuring Download URLs

The public package downloads URL can be updated by editing the `birt.runtime.download.url` and `eclipse.dtp.download.url` properties
specified in the [`pom.xml`](download-birt-package/pom.xml) of the `download-birt-package` module:
```xml
<birt.runtime.download.url>
  https://mirror.umd.edu/eclipse/birt/updates/release/4.18.0/downloads/birt-runtime-4.18.0-202412050604.zip
</birt.runtime.download.url>
```
```xml
<eclipse.dtp.download.url>
   https://eclipse.mirror.wearetriple.com//datatools/updates/release/1.16.3/Data-Tools-Platform-Updates-1.16.3.zip
</eclipse.dtp.download.url>
```

### Deployment Artifacts

After running the command, the deployment artifacts will be available in the `[reportEngine](common/reportEngine)` folder.

### Installing the Component Archetype

First, install the BIRT component archetype:

   ```bash
  cd birt-component-archetype
  mvn install

   ```
### Creating BIRT Component Deployment Modules

Use the following commands to generate deployment modules for each BIRT component:

```bash
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.18.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-birt-runtime -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.birt.runtime_4.18.0-202412050604.jar -DbirtComponentArtifactId=birt-runtime -DbirtComponentVersion=4.18.0
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.18.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-core-contenttype -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.core.contenttype_3.9.600.v20241001-1711.jar -DbirtComponentArtifactId=eclipse-core-contenttype -DbirtComponentVersion=3.9.600
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.18.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-core-expressions -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.core.expressions_3.9.400.v20240413-1529.jar -DbirtComponentArtifactId=eclipse-core-expressions -DbirtComponentVersion=3.9.400
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.18.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-core-filesystem -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.core.filesystem_1.11.100.v20241022-0806.jar -DbirtComponentArtifactId=eclipse-core-filesystem -DbirtComponentVersion=1.11.100
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.18.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-core-jobs -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.core.jobs_3.15.400.v20240619-0602.jar -DbirtComponentArtifactId=eclipse-core-jobs -DbirtComponentVersion=3.15.400
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.18.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-core-resources -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.core.resources_3.22.0.v20241001-1711.jar -DbirtComponentArtifactId=eclipse-core-resources -DbirtComponentVersion=3.22.0
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.18.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-core-runtime -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.core.runtime_3.32.0.v20241003-0436.jar -DbirtComponentArtifactId=eclipse-core-runtime -DbirtComponentVersion=3.32.0
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.18.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-datatools-connectivity-apache-derby -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.datatools.connectivity.apache.derby_1.3.0.202311071249.jar -DbirtComponentArtifactId=eclipse-datatools-connectivity-apache-derby -DbirtComponentVersion=1.3.0
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.18.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-datatools-connectivity-oda-consumer -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.datatools.connectivity.oda.consumer_3.5.0.202311071249.jar -DbirtComponentArtifactId=eclipse-datatools-connectivity-oda-consumer -DbirtComponentVersion=3.5.0
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.18.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-datatools-connectivity-oda-design -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.datatools.connectivity.oda.design_3.6.0.202311071249.jar -DbirtComponentArtifactId=eclipse-datatools-connectivity-oda-design -DbirtComponentVersion=3.6.0
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.18.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-datatools-connectivity-oda-profile -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.datatools.connectivity.oda.profile_3.5.0.202311071249.jar -DbirtComponentArtifactId=eclipse-datatools-connectivity-oda-profile -DbirtComponentVersion=3.5.0
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.18.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-datatools-connectivity-oda -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.datatools.connectivity.oda_3.7.0.202311071249.jar -DbirtComponentArtifactId=eclipse-datatools-connectivity-oda -DbirtComponentVersion=3.7.0
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.18.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-datatools-connectivity-sqm-core -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.datatools.connectivity.sqm.core_1.6.0.202311071345.jar -DbirtComponentArtifactId=eclipse-datatools-connectivity-sqm-core -DbirtComponentVersion=1.6.0
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.18.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-datatools-connectivity -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.datatools.connectivity_1.15.0.202311071249.jar -DbirtComponentArtifactId=eclipse-datatools-connectivity -DbirtComponentVersion=1.15.0
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.18.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-emf-common -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.emf.common_2.40.0.v20240911-1027.jar -DbirtComponentArtifactId=eclipse-emf-common -DbirtComponentVersion=2.40.2
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.18.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-emf-ecore-change -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.emf.ecore.change_2.17.0.v20240604-0832.jar -DbirtComponentArtifactId=eclipse-emf-ecore-change -DbirtComponentVersion=2.17.0
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.18.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-emf-ecore-xmi -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.emf.ecore.xmi_2.38.0.v20240721-0634.jar -DbirtComponentArtifactId=eclipse-emf-ecore-xmi -DbirtComponentVersion=2.38.0
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.18.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-emf-ecore -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.emf.ecore_2.38.0.v20241018-1213.jar -DbirtComponentArtifactId=eclipse-emf-ecore -DbirtComponentVersion=2.38.0
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.18.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-equinox-app -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.equinox.app_1.7.200.v20240722-2103.jar -DbirtComponentArtifactId=eclipse-equinox-app -DbirtComponentVersion=1.7.200
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.18.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-equinox-common -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.equinox.common_3.19.200.v20241004-0654.jar -DbirtComponentArtifactId=eclipse-equinox-common -DbirtComponentVersion=3.19.200
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.18.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-equinox-event -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.equinox.event_1.7.100.v20240321-1445.jar -DbirtComponentArtifactId=eclipse-equinox-event -DbirtComponentVersion=1.7.100
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.18.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-equinox-preferences -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.equinox.preferences_3.11.200.v20240911-1044.jar -DbirtComponentArtifactId=eclipse-equinox-preferences -DbirtComponentVersion=3.11.200
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.18.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-equinox-registry -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.equinox.registry_3.12.200.v20241004-0654.jar -DbirtComponentArtifactId=eclipse-equinox-registry -DbirtComponentVersion=3.12.200
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.18.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-equinox-simpleconfigurator -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.equinox.simpleconfigurator_1.5.300.v20240424-1301.jar -DbirtComponentArtifactId=eclipse-equinox-simpleconfigurator -DbirtComponentVersion=1.5.300
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.18.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-jetty-servlet-api -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.jetty.servlet-api_4.0.6.jar -DbirtComponentArtifactId=eclipse-jetty-servlet-api -DbirtComponentVersion=4.0.6
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.18.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-orbit-xml-apis -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.orbit.xml-apis-ext_1.0.0.v20240917-0534.jar -DbirtComponentArtifactId=eclipse-orbit-xml-apis -DbirtComponentVersion=1.0.0
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.18.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-osgi -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.osgi_3.22.0.v20241030-2121.jar -DbirtComponentArtifactId=eclipse-osgi -DbirtComponentVersion=3.22.0
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.18.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-datatools-enablement-oda-xml -Dversion=1.0.0 -DsrcJar=addons/org.eclipse.datatools.enablement.oda.xml_1.6.0.202411281604.jar -DbirtComponentArtifactId=eclipse-datatools-enablement-oda-xml -DbirtComponentVersion=1.6.0
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.18.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-datatools-modelbase-dbdefinition -Dversion=1.0.0 -DsrcJar=addons/org.eclipse.datatools.modelbase.dbdefinition_1.3.0.202311071249.jar -DbirtComponentArtifactId=eclipse-datatools-modelbase-dbdefinition -DbirtComponentVersion=1.3.0
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.18.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-eclipse-datatools-modelbase-derby -Dversion=1.0.0 -DsrcJar=addons/org.eclipse.datatools.modelbase.derby_1.3.0.202311071249.jar -DbirtComponentArtifactId=eclipse-datatools-modelbase-derby -DbirtComponentVersion=1.3.0
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.18.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-eclipse-datatools-modelbase-sql-query -Dversion=1.0.0 -DsrcJar=addons/org.eclipse.datatools.modelbase.sql.query_1.4.0.202311071249.jar -DbirtComponentArtifactId=eclipse-datatools-modelbase-sql-query -DbirtComponentVersion=1.4.0
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.18.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-datatools-modelbase-sql -Dversion=1.0.0 -DsrcJar=addons/org.eclipse.datatools.modelbase.sql_1.3.0.202311071249.jar -DbirtComponentArtifactId=eclipse-datatools-modelbase-sql -DbirtComponentVersion=1.3.0
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.18.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-icu -Dversion=1.0.0 -DsrcJar=lib/com.ibm.icu_76.1.0.jar -DbirtComponentArtifactId=icu -DbirtComponentVersion=76.1.0
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.18.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-jna -Dversion=1.0.0 -DsrcJar=lib/com.sun.jna.platform_5.15.0.jar -DbirtComponentArtifactId=jna -DbirtComponentVersion=5.15.0
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.18.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-wsdl -Dversion=1.0.0 -DsrcJar=lib/javax.wsdl_1.6.3.v20230730-0710.jar -DbirtComponentArtifactId=wsdl -DbirtComponentVersion=1.6.3
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.18.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-rpc-api -Dversion=1.0.0 -DsrcJar=lib/javax.xml.rpc-api_1.1.4.jar -DbirtComponentArtifactId=rpc-api -DbirtComponentVersion=1.1.4
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.18.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-apache-axis -Dversion=1.0.0 -DsrcJar=lib/org.apache.axis_1.4.1.v20231107-0937.jar -DbirtComponentArtifactId=apache-axis -DbirtComponentVersion=1.4.1
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.18.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-apache-derby -Dversion=1.0.0 -DsrcJar=lib/org.apache.derby_10.16.1.v20240802-0900.jar -DbirtComponentArtifactId=apache-derby -DbirtComponentVersion=10.16.1
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.18.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-mongodb-java-driver -Dversion=1.0.0 -DsrcJar=lib/org.mongodb.mongo-java-driver_3.12.14.jar -DbirtComponentArtifactId=mongodb-java-driver -DbirtComponentVersion=3.12.14
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.18.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-datatools-connectivity-oda-flatfile -Dversion=1.0.0 -DsrcJar=plugins/org.eclipse.datatools.connectivity.oda.flatfile_3.4.0.202311071249.jar -DbirtComponentArtifactId=eclipse-datatools-enablement-oda-flatfile -DbirtComponentVersion=3.4.0
```
Each command creates a deployment module for a specific BIRT or Eclipse component that will be used in the runtime bundle.

## Generate deployment packages

To generate a package ready to be uploaded to Maven Central for each artifact,
execute `mvn package` command on the [deploy-birt-components](deploy-birt-components)
module. This will generate the zip bundle to deploy on Maven central in `target` directory
of each subproject.

## Publishing

### Publishing to internal repository 

To publish to internal repository, activate the `maven-central` profile.

`mvn deploy -Pinternal`

### Publishing to Maven Central

To publish to Maven Central, activate the `maven-central` profile.

To effectively publish the artifact to Maven Central,
it will have to be manually released in the https://central.sonatype.org platform

`mvn deploy -Pmaven-central`
