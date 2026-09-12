pipeline {

    agent any

    stages {

     
        stage('Install Dependencies') {
    agent {
        docker { image 'python:3.11' }
    }
    steps {
        sh 'pip install -r requirements.txt'
    }
}

        
        stage('Run Tests') {

            steps {

                sh '''
                pytest
                '''

            }

        }

        stage('Build Docker Image') {

            steps {

                sh '''
                docker build -t flask-devops-app .
                '''

            }

        }

        stage('Deploy Container') {

            steps {

                sh '''
                docker stop flask-container || true

                docker rm flask-container || true

                docker run -d \
                -p 5000:5000 \
                --name flask-container \
                flask-devops-app
                '''

            }

        }

    }

}
