pipeline {
    options { disableConcurrentBuilds() }
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

                        sh (
                        label: './mvnw deploy spring-boot:build-image',
                        script: 'export OTEL_TRACES_EXPORTER="otlp" && ./mvnw deploy')
                        archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
                    }
                }
            }
        }
    }
}
