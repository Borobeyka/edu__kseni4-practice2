pipeline {
    agent {
        label 'docker'
    }
    stages {
        stage('Build') {
            steps {
                script {
                    docker.image('maven:3.6.3-jdk-8-slim').inside('-u root') {
                        sh 'mvn clean package'
                    }
                }
            }
        }
        stage('Publish Artifact') {
            steps {
                script {
                    archiveArtifacts(artifacts: '**/target/*.jar', fingerprint: true)
                }
            }
        }
    }
    post {
        success {
            echo 'Build successful!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
