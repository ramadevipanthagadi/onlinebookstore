pipeline {
    agent any

    tools {
        maven 'mymave'
    }

    environment {
        DOCKER_USER = 'sunithriyansh'
        DOCKER_PASS = 'Sunitha@565'
        IMAGE_NAME  = 'vidya'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/ramadevipanthagadi/hotstar_project.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t sri .'
            }
        }

        stage('Docker Run') {
            steps {
                sh 'docker rm -f cont1 || true'
                sh 'docker run -d --name cont1 -p 8000:80 sri'
            }
        }

        stage('Push to DockerHub') {
            steps {
                sh 'docker login -u $DOCKER_USER -p $DOCKER_PASS'
                sh 'docker tag imag1:latest $DOCKER_USER/$IMAGE_NAME:latest'
                sh 'docker push $DOCKER_USER/$IMAGE_NAME:latest'
            }
        }

    }
}
