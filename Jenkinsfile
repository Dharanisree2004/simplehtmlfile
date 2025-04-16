pipeline {
    agent any

    environment {
        IMAGE_NAME = 'my-html-app'
        CONTAINER_NAME = 'html-container'
        PORT = '8080'
    }

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/Dharanisree2004/simplehtmlfile.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh '''
                    docker stop $CONTAINER_NAME || true
                    docker rm $CONTAINER_NAME || true
                '''
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d --name $CONTAINER_NAME -p $PORT:80 $IMAGE_NAME'
            }
        }
    }

    post {
        success {
            echo "🚀 Deployed at: http://localhost:$PORT"
        }
        failure {
            echo '❌ Something went wrong!'
        }
    }
}
