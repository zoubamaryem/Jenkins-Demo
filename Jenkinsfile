pipeline {
    // agent any
    agent none

    // tools {
    //     // Install the Maven version configured as "M3" and add it to the path.
    //     maven "M3"
    // }

    // Poll every 5 minutes, if there is a new code Jenkins will run the job
    triggers {
        pollSCM('*/5 * * * *')
    }

    stages {
        // For Pipeline script
        // stage('Clone Repo') {
        //     steps {
        //         // Get some code from a GitHub repository
        //         git branch: 'main', url: 'https://github.com/wahid007/Jenkins-Demo.git'
        //         // git 'https://github.com/wahid007/Jenkins-Demo'
        //     }

        // }
        
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
                echo "demo-jenkins-${env.BUILD_NUMBER}"
                // docker.build demo-jenkins-${env.BUILD_NUMBER}
                sh "docker rmi wahid007/jenkins_demo"
                sh "docker build -t wahid007/jenkins_demo ."
            }
          }
        }     

        stage('Run Docker Container') {
          steps{
            script {
                // delete container if exists
                sh "docker rm -f myContainerName"
                sh "docker run -d --name myContainerName -p 2222:2222 wahid007/jenkins_demo"
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
