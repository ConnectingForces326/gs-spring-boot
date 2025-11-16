pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Build the Spring Boot app inside the "complete" folder
                sh 'mvn -B -f complete/pom.xml clean package'
            }
        }

        stage('Archive Jar') {
            steps {
                // Save the jar file from the "complete/target" folder
                archiveArtifacts artifacts: 'complete/target/*.jar', fingerprint: true
            }
        }
    }
}
