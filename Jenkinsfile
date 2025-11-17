pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Prep') {
            steps {
                // make mvnw executable, ignore error if it already is
                sh 'chmod +x mvnw || true'
            }
        }

        stage('Build') {
            steps {
                sh './mvnw -B -DskipTests clean package'
            }
            post {
                success {
                    archiveArtifacts 'targe
