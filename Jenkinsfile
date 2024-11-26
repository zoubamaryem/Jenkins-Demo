pipeline {
    agent any

    def dockerImage
    def dockerImageTag = "wahid007/demo-jenkins${env.BUILD_NUMBER}"
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
              // echo "demo-jenkins-${env.BUILD_NUMBER}"
              // docker.build demo-jenkins-${env.BUILD_NUMBER}
              //   dockerImage = docker.build dockerimagename
              echo "Docker Image Tag Name: ${dockerImageTag}"
              sh "docker build -t ${dockerImageTag} ."
              // dockerImage = docker.build("${dockerImageTag}")                
            }
          }
        }       

        stage('Deploy Docker Image'){
          steps {
            script {
              sh "docker run --name demo-jenkins -d -p 2222:2222 ${dockerImageTag}"
            }
          }
        } 

        // stage('Push image') {
        //     /* Finally, we'll push the image with the 'latest' tag.
        //      Pushing multiple tags is cheap, as all the layers are reused. */
        //     docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
        //         app.push("${env.BUILD_NUMBER}")
        //         app.push("latest")
        //     }
        // }
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
