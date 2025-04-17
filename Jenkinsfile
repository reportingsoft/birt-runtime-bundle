pipeline {
    agent {
        label "linux"
    }
    environment {
        JDK_TOOL = 'JDK_21'
        MAVEN_TOOL = 'MAVEN'
    }
    stages {
        stage('Download BIRT package') {
            when {
                expression {
                    def dirExists = sh(
                            script: "if [ -d common/reportEngine ]; then echo true; else echo false; fi",
                            returnStdout: true
                    ).trim()
                    return dirExists == "false"
                }
            }
            steps {
                dir("download-birt-package") {
                    withMaven(
                            maven: "${MAVEN_TOOL}",
                            jdk: "${JDK_TOOL}"
                    ) {
                        sh """mvn package -Pdownload-package"""
                    }
                }
            }
        }
        stage('Install Component Archetype') {
            steps {
                dir("birt-component-archetype") {
                    withMaven(
                            maven: "${MAVEN_TOOL}",
                            jdk: "${JDK_TOOL}"
                    ) {
                        sh "mvn install"
                    }
                }
            }
        }
        stage('Generate Component Modules') {
            steps {
                sh '''
                    # Cleanup all subdirectories under deploy-birt-components
                    find deploy-birt-components -mindepth 1 -type d -exec rm -rf {} +
                '''
                dir("deploy-birt-components") {
                    withMaven(
                            maven: "${MAVEN_TOOL}",
                            jdk: "${JDK_TOOL}"
                    ) {
                        sh """
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
                        """
                    }
                }
            }
        }
        stage('Deploy components') {
            steps {
                dir("deploy-birt-components") {
                    withCredentials([file(credentialsId: 'MAVEN_CENTRAL_SIGNING_KEY', variable: 'SIGNING_KEY')]) {
                    withMaven(
                            maven: "${MAVEN_TOOL}",
                            jdk: "${JDK_TOOL}"
                    ) {
                            sh """gpg --allow-secret-key-import --import ${SIGNING_KEY}"""
                        sh "mvn clean deploy"
                    }
                    }
                }
            }
        }
    }
}