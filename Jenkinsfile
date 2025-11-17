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
                sh 'chmod +x mvnw || true'
            }
        }

        stage('Build') {
            steps {
                sh './mvnw -B -DskipTests clean package'
            }
            post {
                success {
                    archiveArtifacts 'target/*.jar'
                }
            }
        }

        stage('Test') {
            steps {
                sh './mvnw -B test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }

        // 🔥 NEW: this is the part that sends the JAR to Nexus
        stage('Upload Jar to Nexus') {
            steps {
                sh '''
                    JAR_FILE=$(ls target/*.jar | head -n 1)
                    echo "Uploading $JAR_FILE to Nexus..."

                    curl -v -u admin:admin123 \
                      --upload-file "$JAR_FILE" \
                      "http://host.docker.internal:8081/repository/maven-releases/com/example/demo/$(basename "$JAR_FILE")"
                '''
            }
        }
    }
}
