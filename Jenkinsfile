node {
    def mvnHome = tool 'maven-3.9.9'
    def dockerImage
    def dockerImageTag = "devopsexample:${env.BUILD_NUMBER}"
    
    stage('Clone Repo') {
        git branch: 'main', url: 'https://github.com/zoubamaryem/Jenkins-Demo.git'
    }
    
    stage('Build Project') {
        sh "${mvnHome}/bin/mvn clean package"
    }
    
    stage('Initialize Docker'){
        def dockerHome = tool 'MyDocker'
        env.PATH = "${dockerHome}/bin:${env.PATH}"
    }
    
    stage('Build Docker Image') {
        sh "docker -H tcp://192.168.100.34:2375 build -t ${dockerImageTag} ."
    }
    
    stage('Deploy Docker Image'){
        echo "Docker Image Tag Name: ${dockerImageTag}"
        sh "docker -H tcp://192.168.100.34:2375 run --name devopsexample-${env.BUILD_NUMBER} -d -p 2222:2222 ${dockerImageTag}"
    }
}
