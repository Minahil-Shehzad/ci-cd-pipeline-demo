pipeline {
    agent any

    environment {
        GITHUB_TOKEN = credentials('github-token')
    }

    stages {
        stage('Clone Repository') {
            steps {
                // Clone using the token
                git url: 'https://github.com/Minahil-Shehzad/ci-cd-pipeline-demo.git', 
                    credentialsId: 'github-token', 
                    branch: 'main'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'pytest tests/'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t minahil/ci-cd-demo:latest .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker run -d -p 5000:5000 minahil/ci-cd-demo:latest'
            }
        }
    }
}

