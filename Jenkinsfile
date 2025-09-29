pipeline {
    agent any

    environment {
        BACKEND_IMAGE = "paragkulkarni4549/easycrud-backend"
        FRONTEND_IMAGE = "paragkulkarni4549/easycrud-frontend"
    }

    stages {
        stage('Clone Code') {
            steps {
                git branch: 'main', url: 'git@github.com:paragkulkarni4549/EasyCRUD.git'
            }
        }

        stage('Build Backend Docker Image') {
            steps {
                script {
                    sh 'docker build -t $BACKEND_IMAGE -f Dockerfile.backend .'
                }
            }
        }

        stage('Build Frontend Docker Image') {
            steps {
                script {
                    sh 'docker build -t $FRONTEND_IMAGE -f Dockerfile.frontend .'
                }
            }
        }

        stage('Run Containers') {
            steps {
                script {
                    // Backend चालू कर
                    sh '''
                    docker rm -f backend || true
                    docker run -d --name backend -p 8080:8080 $BACKEND_IMAGE
                    '''

                    // Frontend चालू कर
                    sh '''
                    docker rm -f frontend || true
                    docker run -d --name frontend -p 80:80 --link backend $FRONTEND_IMAGE
                    '''
                }
            }
        }
    }
}
