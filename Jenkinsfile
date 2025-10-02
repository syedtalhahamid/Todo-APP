pipeline {
    agent any

   

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/syedtalhahamid/Todo-APP.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                    docker build -t Todo-APP:latest .
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                    # Stop old container if running
                    docker stop Todo-APP-container || true
                    docker rm Todo-APP-container || true

                    # Run new container
                    docker run -d --name Todo-APP-container -p 5000:5000 Todo-APP-container:latest
                '''
            }
        }
    }

    post {
        success {
            echo "✅ TodoApp is running at http://localhost:5000"
        }
        failure {
            echo "❌ Build or run failed!"
        }
    }
}
