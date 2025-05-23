# BIRT Runtime Bundle

This repository manages the generation and publication of BIRT Runtime libraries.

## Import the Bundle in your project

The [birt-runtime](birt-runtime) module provides all necessary dependencies
to run a BIRT engine in your Java application.

All dependencies declared in the [pom.xml](birt-runtime/pom.xml) file will be transitively available to projects that include `birt-runtime-bundle` as a dependency:


**Gradle**

    compile (group: 'ch.reportingsoft.birt', name: 'birt-runtime-bundle', version: '4.19.0')

**Maven**

    <dependency>
        <groupId>ch.reportingsoft.birt</groupId>
        <name>birt-runtime-bundle</name>
        <version>4.19.0</version>
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
   https://eclipse.mirror.wearetriple.com//birt/updates/release/4.19.0/downloads/birt-runtime-4.19.0-202503120947.zip
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
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.19.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-birt-runtime -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.birt.runtime_4.19.0-202503120947.jar -DbirtComponentArtifactId=birt-runtime -DbirtComponentVersion=4.19.0
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.19.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-core-jobs -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.core.jobs_3.15.500.v20250204-0817.jar -DbirtComponentArtifactId=eclipse-core-jobs -DbirtComponentVersion=3.15.500
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.19.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-core-resources -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.core.resources_3.22.100.v20250206-1238.jar -DbirtComponentArtifactId=eclipse-core-resources -DbirtComponentVersion=3.22.100
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.19.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-core-runtime -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.core.runtime_3.33.0.v20250206-0919.jar -DbirtComponentArtifactId=eclipse-core-runtime -DbirtComponentVersion=3.33.0
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.19.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-datatools-connectivity-apache-derby -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.datatools.connectivity.apache.derby_1.3.0.202412071309.jar -DbirtComponentArtifactId=eclipse-datatools-connectivity-apache-derby -DbirtComponentVersion=1.3.0.2024
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.19.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-datatools-connectivity-sqm-core -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.datatools.connectivity.sqm.core_1.6.0.202412071309.jar -DbirtComponentArtifactId=eclipse-datatools-connectivity-sqm-core -DbirtComponentVersion=1.6.0.2024
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.19.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-emf-common -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.emf.common_2.41.0.v20241204-1554.jar -DbirtComponentArtifactId=eclipse-emf-common -DbirtComponentVersion=2.41.0
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.19.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-equinox-app -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.equinox.app_1.7.300.v20250130-0528.jar -DbirtComponentArtifactId=eclipse-equinox-app -DbirtComponentVersion=1.7.300
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.19.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-equinox-common -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.equinox.common_3.20.0.v20250129-1348.jar -DbirtComponentArtifactId=eclipse-equinox-common -DbirtComponentVersion=3.20.0
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.19.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-equinox-event -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.equinox.event_1.7.200.v20250129-1349.jar -DbirtComponentArtifactId=eclipse-equinox-event -DbirtComponentVersion=1.7.200
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.19.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-equinox-preferences -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.equinox.preferences_3.11.300.v20250130-0533.jar -DbirtComponentArtifactId=eclipse-equinox-preferences -DbirtComponentVersion=3.11.300                           
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.19.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-equinox-registry -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.equinox.registry_3.12.300.v20250129-1129.jar -DbirtComponentArtifactId=eclipse-equinox-registry -DbirtComponentVersion=3.12.300
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.19.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-equinox-simpleconfigurator -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.equinox.simpleconfigurator_1.5.400.v20250129-0942.jar -DbirtComponentArtifactId=eclipse-equinox-simpleconfigurator -DbirtComponentVersion=1.5.400                          
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.19.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-osgi -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.osgi_3.23.0.v20250228-0640.jar -DbirtComponentArtifactId=eclipse-osgi -DbirtComponentVersion=3.23.0
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.19.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-datatools-modelbase-dbdefinition -Dversion=1.0.0 -DsrcJar=addons/org.eclipse.datatools.modelbase.dbdefinition_1.3.0.202412071309.jar -DbirtComponentArtifactId=eclipse-datatools-modelbase-dbdefinition -DbirtComponentVersion=1.3.0.2024
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.19.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-datatools-modelbase-derby -Dversion=1.0.0 -DsrcJar=addons/org.eclipse.datatools.modelbase.derby_1.3.0.202412071309.jar -DbirtComponentArtifactId=eclipse-datatools-modelbase-derby -DbirtComponentVersion=1.3.0.2024
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.19.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-datatools-modelbase-sql-query -Dversion=1.0.0 -DsrcJar=addons/org.eclipse.datatools.modelbase.sql.query_1.4.0.202412071309.jar -DbirtComponentArtifactId=eclipse-datatools-modelbase-sql-query -DbirtComponentVersion=1.4.0.2024
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.19.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-datatools-modelbase-sql -Dversion=1.0.0 -DsrcJar=addons/org.eclipse.datatools.modelbase.sql_1.3.0.202412071309.jar -DbirtComponentArtifactId=eclipse-datatools-modelbase-sql -DbirtComponentVersion=1.3.0.2024
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.19.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-jna -Dversion=1.0.0 -DsrcJar=lib/com.sun.jna.platform_5.16.0.jar -DbirtComponentArtifactId=jna -DbirtComponentVersion=5.16.0 
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
