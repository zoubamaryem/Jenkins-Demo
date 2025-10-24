pipeline {
    agent any

    tools {
        jdk 'JDK'
        maven 'maven-3.9.9'
    }

    environment {
        DOCKER_HOST = "tcp://127.0.0.1:2375"
        DOCKER_CLI_HINTS = "false"
    }

    stages {

        stage('Checkout SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/zoubamaryem/Jenkins-Demo.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t jenkins-demo-app .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                    docker rm -f jenkins-demo-container || true
                    docker run -d --name jenkins-demo-container -p 2222:8080 jenkins-demo-app
                '''
            }
        }
    }

    post {
        failure {
            echo "Le pipeline a échoué. Vérifiez les logs."
        }
        success {
            echo "Pipeline exécuté avec succès. Application disponible sur le port 2222."
        }
    }
}
