pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Fetch the code from the repository
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Use Maven to build the project
                sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                // Run tests using Maven
                sh 'mvn test'
            }
        }
        
        stage('Archive') {
            steps {
                // Archive build artifacts, such as JAR files
                archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
            }
        }
    }

    post {
        always {
            // Clean up workspace if needed
            cleanWs()
        }

        success {
            echo 'Build and tests completed successfully.'
        }

        unstable {
            echo 'Build completed, but there were some test failures.'
        }

        failure {
            echo 'Build or tests failed.'
        }

        changed {
            echo 'The build result has changed.'
        }
    }
}

