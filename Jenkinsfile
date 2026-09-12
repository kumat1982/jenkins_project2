pipeline {

    agent any

    stages {

     
        stage('Install Dependencies') {
    steps {
        sh '''
            python3 -m venv venv
            . venv/bin/activate
            pip install -r requirements.txt
        '''
    }
}
stage('Run Tests') {
    steps {
        sh '''
            . venv/bin/activate
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
