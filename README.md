# BIRT Runtime Bundle
This repository is responsible for generating and publishing BIRT Runtime libraries.

---

## Download BIRT Package

To download the BIRT package, use the following steps:

1. Navigate to the `[birt-deploy-parent](birt-deploy-parent)` module.
2. Run the following Maven command:
   ```bash
   mvn clean package -Pdownload-package
   ```
   This command will:
    - Download the BIRT public package using the URL specified in the [`pom.xml`](birt-deploy-parent/pom.xml).
    - Unpack the downloaded package into the `target` directory.

The public package download URL can be updated by editing the `birt.runtime.download.url` property:
```xml
<birt.runtime.download.url>
  https://mirror.umd.edu/eclipse/birt/updates/release/4.18.0/downloads/birt-runtime-4.18.0-202412050604.zip
</birt.runtime.download.url>
```

### Location of Downloaded Artifacts

After running the command, the deployment artifacts will be available in the `[reportEngine](birt-deploy-parent/target/reportEngine)` folder.

---

## Create a BIRT Component Deployment Artifact

To create a BIRT component deployment artifact, execute the following Maven command:

```bash
mvn -U archetype:generate \
    -DinteractiveMode=true \
    -DarchetypeGroupId=ch.reportingsoft.birt \
    -DarchetypeArtifactId=birt-component-archetype \
    -DarchetypeVersion=1.0-SNAPSHOT \
    -DgroupId=ch.reportingsoft.birt \
    -Dversion=1.0.0-SNAPSHOT \
    -DartifactId=<artifact-id> \
    -DsrcJar=<path-to-birt-component-jar> \
    -DbirtComponentArtifactId=<component-artifact-id> \
    -DbirtComponentVersion=<component-version>
```

This command will create a deployment artifact based on the specified archetype, allowing you to customize the parameters like `groupId`, `artifactId`, `version`, and `package` as needed.

```
mvn -U archetype:generate -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=1.0-SNAPSHOT -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-core-contenttype -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.core.contenttype_3.9.600.v20241001-1711.jar -DbirtComponentArtifactId=eclipse-core-contenttype -DbirtComponentVersion=3.9.600
mvn -U archetype:generate -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=1.0-SNAPSHOT -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-core-expressions -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.core.expressions_3.9.400.v20240413-1529.jar -DbirtComponentArtifactId=eclipse-core-expressions -DbirtComponentVersion=3.9.400
mvn -U archetype:generate -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=1.0-SNAPSHOT -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-core-filesystem -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.core.filesystem_1.11.100.v20241022-0806.jar -DbirtComponentArtifactId=eclipse-core-filesystem -DbirtComponentVersion=1.11.100
mvn -U archetype:generate -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=1.0-SNAPSHOT -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-core-runtime -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.core.runtime_3.32.0.v20241003-0436.jar -DbirtComponentArtifactId=eclipse-core-runtime -DbirtComponentVersion=3.32.0
```

---

### Notes

- For further details, refer to the `birt-deploy-parent` module documentation.
- Ensure you have the required dependencies and permissions before executing the above commands.