pipeline {
    agent any
    
    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/your-repo/hello-world.git' // Replace with your repository URL
            }
        }
        
        stage('Build') {
            steps {
                withMaven(maven: 'M3') {
                    sh 'mvn clean package'
                }
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                // Add deployment steps if any, such as copying to a server or using Docker
            }
        }
    }
}
