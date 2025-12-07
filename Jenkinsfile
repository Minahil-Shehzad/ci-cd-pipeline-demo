pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'minahilshahzad123/ci-cd-pipeline-demo:latest'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Minahil-Shehzad/ci-cd-pipeline-demo.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Example: npm install
                sh 'npm install'
                // If you have Python: sh 'pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                // Example: run test scripts in /tests folder
                sh 'npm test'
                // Or Python: sh 'pytest tests/'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-creds') {
                        docker.image("${DOCKER_IMAGE}").push()
                    }
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
