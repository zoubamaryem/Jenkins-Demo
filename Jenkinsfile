pipeline {
    agent any

    environment {
        // The MY_KUBECONFIG environment variable will be assigned
        // the value of a temporary file.  For example:
        //   /home/user/.jenkins/workspace/cred_test@tmp/secretFiles/546a5cf3-9b56-4165-a0fd-19e2afe6b31f/kubeconfig.txt
        // MY_KUBECONFIG = credentials('my-kubeconfig')
        registry = "wahid007/demo-jenkins"
        registryCredential = 'dockerhub_id'
        dockerImage = ''        
    }


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
              // sh "docker build -t $registry:$BUILD_NUMBER ."
              script {
                dockerImage = docker.build registry + ":$BUILD_NUMBER"   
              }          
          }
        }       

        stage('Deploy Docker Image'){
          steps {
            sh "docker run --name demo-jenkins -d -p 2222:2222 $registry:$BUILD_NUMBER"
          }
        }

        // stage('Push image') {
          // steps{
          //   script {
        //     /* Finally, we'll push the image with the 'latest' tag.
        //      Pushing multiple tags is cheap, as all the layers are reused. */
        //     docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
              //  dockerImage.push()
        //     }
//     }
// }
        // }

        // stage('Cleaning up') {
        //   steps{
        //     sh "docker rmi $registry:$BUILD_NUMBER"
        //   }
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
