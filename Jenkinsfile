
pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code from GitHub...'
                checkout scm
            }
        }

        stage('Verify Environment') {
            steps {
                echo 'Checking Java version...'
                sh 'java -version'

                echo 'Checking Maven version...'
                sh 'mvn -version'
            }
        }

        stage('Build') {
            steps {
                echo 'Building Spring Boot application...'
                sh 'mvn clean package'
            }
        }

        stage('Archive Artifact') {
            steps {
                echo 'Archiving generated JAR...'

                archiveArtifacts(
                    artifacts: 'target/*.jar',
                    fingerprint: true
                )
            }
        }
    }

    post {
        success {
            echo 'BUILD SUCCESSFUL!'
            echo 'Spring Boot application packaged successfully.'
        }

        failure {
            echo 'BUILD FAILED!'
            echo 'Please check the Jenkins console output.'
        }
    }
}
