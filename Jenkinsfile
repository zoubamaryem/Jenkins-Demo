pipeline {
    agent any

    // tools {
    //     // Install the Maven version configured as "M3" and add it to the path.
    //     maven "M3"
    // }

    stages {
        stage('Clone Repo') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/wahid007/Jenkins-Demo.git'
            }

        }
        
        stage('Build App') {
            steps {
                // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }

        }
        
        stage('Build image') {
          steps{
            script {
            //   dockerImage = docker.build dockerimagename
                echo "devopsexample-${env.BUILD_NUMBER}"
            }
          }
        }        
    }
    
    post {
        success {
            echo 'Pipeline execution successful!'
        }
        failure {
            echo 'Pipeline execution failed.'
        }
    }    
}
