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
                             mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.20.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-jna -Dversion=1.0.0 -DsrcJar=lib/com.sun.jna.platform_5.17.0.jar -DbirtComponentArtifactId=jna -DbirtComponentVersion=5.17.0
                             mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.20.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-core-filesystem -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.core.filesystem_1.11.200.v20250513-1234.jar -DbirtComponentArtifactId=eclipse-core-filesystem -DbirtComponentVersion=1.11.200
                             mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.20.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-core-resources -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.core.resources_3.22.200.v20250513-1234.jar -DbirtComponentArtifactId=eclipse-core-resources -DbirtComponentVersion=3.22.200
                             mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.20.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-emf-common -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.emf.common_2.42.0.v20250401-0947.jar -DbirtComponentArtifactId=eclipse-emf-common -DbirtComponentVersion=2.42.0
                             mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.20.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-emf-ecore-xmi -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.emf.ecore.xmi_2.39.0.v20250414-1351.jar -DbirtComponentArtifactId=eclipse-emf-ecore-xmi -DbirtComponentVersion=2.39.0
                             mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.20.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-emf-ecore -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.emf.ecore_2.39.0.v20250401-0947.jar -DbirtComponentArtifactId=eclipse-emf-ecore -DbirtComponentVersion=2.39.0
                             mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.20.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-equinox-event -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.equinox.event_1.7.300.v20250518-0609.jar -DbirtComponentArtifactId=eclipse-equinox-event -DbirtComponentVersion=1.7.300
                             mvn -U archetype:generate -DinteractiveMode=false -DarchetypeGroupId=ch.reportingsoft.birt -DarchetypeArtifactId=birt-component-archetype -DarchetypeVersion=4.20.0 -DgroupId=ch.reportingsoft.birt -DartifactId=deploy-eclipse-equinox-simpleconfigurator -Dversion=1.0.0 -DsrcJar=lib/org.eclipse.equinox.simpleconfigurator_1.5.500.v20250306-1127.jar -DbirtComponentArtifactId=eclipse-equinox-simpleconfigurator -DbirtComponentVersion=1.5.500
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