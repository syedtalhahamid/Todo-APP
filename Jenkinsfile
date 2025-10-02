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
                bat '''
                    docker build -t todo-app:latest .
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                bat '''
                    # Stop old container if running
                    docker stop todo-app-container || true
                    docker rm todo-app-container || true

                    # Run new container
                    docker run -d --name todo-app-container -p 5000:5000 todo-app:latest
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
