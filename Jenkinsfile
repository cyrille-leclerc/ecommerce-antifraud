pipeline {
    options {
      buildDiscarder logRotator(numToKeepStr: '4')
      disableConcurrentBuilds()
    }
    agent {
      label 'linux'
    }
    stages {
        stage('Build') {
            steps {
                withCredentials([string(credentialsId: 'snyk.io', variable: 'SNYK_TOKEN')]) {
                    withCredentials([
                        usernamePassword(
                            credentialsId: 'docker.io',
                            passwordVariable: 'CONTAINER_REGISTRY_PASSWORD',
                            usernameVariable: 'CONTAINER_REGISTRY_USERNAME')]) {

                        // sh (
                        // label: 'mvn deploy spring-boot:build-image',
                        //script: './mvnw deploy')
                                               // sh (
                        // label: 'mvn package',
                        //script: './mvnw package')
                        archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
                    }
                }
            }
        }
    }
}
