pipeline {
    agent {
        label "linux"
    }
    environment {
        JDK_TOOL = 'JDK_21'
        MAVEN_TOOL = 'MAVEN'
    }
    stages {
        stage('Build Package') {
            steps {
                dir ("download-birt-package") {
                    withMaven(
                            maven: "${MAVEN_TOOL}",
                            jdk: "${JDK_TOOL}"
                    ) {
                        sh """mvn package -Pdownload-package"""
                    }
                }
            }
        }
    }
}