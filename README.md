# BIRT Runtime Bundle

This repository manages the generation and publication of BIRT Runtime libraries.

## Import the Bundle in your project

The [birt-runtime](birt-runtime) module provides all necessary dependencies
to run a BIRT engine in your Java application.

All dependencies declared in the [pom.xml](birt-runtime/pom.xml) file will be transitively available to projects that include `birt-runtime-bundle` as a dependency:


**Gradle**

    compile (group: 'ch.reportingsoft.birt', name: 'birt-runtime-bundle', version: '4.20.0')

**Maven**

    <dependency>
        <groupId>ch.reportingsoft.birt</groupId>
        <name>birt-runtime-bundle</name>
        <version>4.20.0</version>
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
   https://mirrors.dotsrc.org/eclipse//birt/updates/release/4.20.0/downloads/birt-runtime-4.20.0-202506110821.zip
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
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.20.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-birt-runtime -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.birt.runtime_4.20.0-202506110821.jar -DbirtComponentArtifactId=birt-runtime -DbirtComponentVersion=4.20.0
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.20.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-jna -Dversion=1.0.0 -DsrcJar=lib/com.sun.jna.platform_5.17.0.jar -DbirtComponentArtifactId=jna -DbirtComponentVersion=5.17.0 
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.20.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-core-filesystem -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.core.filesystem_1.11.200.v20250513-1234.jar -DbirtComponentArtifactId=eclipse-core-filesystem -DbirtComponentVersion=1.11.200 
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.20.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-core-resources -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.core.resources_3.22.200.v20250513-1234.jar -DbirtComponentArtifactId=eclipse-core-resources -DbirtComponentVersion=3.22.200
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.20.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-emf-common -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.emf.common_2.42.0.v20250401-0947.jar -DbirtComponentArtifactId=eclipse-emf-common -DbirtComponentVersion=2.42.0
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.20.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-emf-ecore-xmi -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.emf.ecore.xmi_2.39.0.v20250414-1351.jar -DbirtComponentArtifactId=eclipse-emf-ecore-xmi -DbirtComponentVersion=2.39.0
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.20.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-emf-ecore -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.emf.ecore_2.39.0.v20250401-0947.jar -DbirtComponentArtifactId=eclipse-emf-ecore -DbirtComponentVersion=2.39.0
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.20.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-equinox-event -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.equinox.event_1.7.300.v20250518-0609.jar -DbirtComponentArtifactId=eclipse-equinox-event -DbirtComponentVersion=1.7.300
 mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.20.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-equinox-simpleconfigurator -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.equinox.simpleconfigurator_1.5.500.v20250306-1127.jar -DbirtComponentArtifactId=eclipse-equinox-simpleconfigurator -DbirtComponentVersion=1.5.500                          
```
Each command creates a deployment module for a specific BIRT or Eclipse component that will be used in the runtime bundle.

## Generate deployment packages

To generate a package ready to be uploaded to Maven Central for each artifact,
execute `mvn package` command on the [deploy-birt-components](deploy-birt-components)
module. This will generate the zip bundle to deploy on Maven central in `target` directory
of each subproject.

## Publishing

### Publishing to internal repository 

To publish to internal repository, activate the `internal` profile.

`mvn deploy -Pinternal`

### Publishing to Maven Central

To publish to Maven Central, activate the `maven-central` profile.

To effectively publish the artifact to Maven Central,
it will have to be manually released in the https://central.sonatype.org platform

`mvn deploy -Pmaven-central`
