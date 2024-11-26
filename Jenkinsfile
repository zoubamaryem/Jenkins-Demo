node {
    def dockerImage
    def dockerImageTag = "wahid007/demo-jenkins${env.BUILD_NUMBER}"
    
    stage('Clone Repo') {
      git 'https://github.com/wahid007/Jenkins-Demo.git'
    }    
  
    stage('Build Project') {
      sh "mvn -Dmaven.test.failure.ignore=true clean package"
    }
    
    stage('Build Docker Image') {
      //   dockerImage = docker.build dockerimagename
      echo "Docker Image Tag Name: ${dockerImageTag}"
      sh "docker build -t ${dockerImageTag} ."
      // dockerImage = docker.build("${dockerImageTag}")
    }
    
    stage('Deploy Docker Image'){
	    sh "docker run --name demo-jenkins -d -p 2222:2222 ${dockerImageTag}"
    }

    // stage('Push image') {
    //     /* Finally, we'll push the image with the 'latest' tag.
    //      Pushing multiple tags is cheap, as all the layers are reused. */
    //     docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
    //         app.push("${env.BUILD_NUMBER}")
    //         app.push("latest")
    //     }
    // }    

    post {
        success {
            echo 'Pipeline execution successful!'
        }
        failure {
            echo 'Pipeline execution failed.'
        }
    }    
}
