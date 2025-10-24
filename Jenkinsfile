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
```

5. **Cliquez sur "Commit changes"** (en haut à droite)

6. Dans la popup, cliquez sur **"Commit changes"** pour confirmer

---

# 🚀 **ÉTAPE 15 : CRÉER LE PIPELINE DANS JENKINS**

Maintenant, retournez sur Jenkins.

## 15.1 Créer le Pipeline

1. Allez sur le Dashboard Jenkins : `http://192.168.100.34:8080/`
2. Cliquez sur **"Nouveau Item"** ou **"New Item"** (menu gauche)

3. **Remplissez :**
   - **Nom** : `Jenkins-Demo-Pipeline`
   - **Type** : Sélectionnez **"Pipeline"**
   - Cliquez sur **"OK"**

---

## 15.2 Configuration du Pipeline

### **Section "General"**

1. ✅ Cochez **"GitHub project"**
2. **Project url** : 
```
   https://github.com/zoubamaryem/Jenkins-Demo/
```

### **Section "Pipeline"**

Descendez jusqu'à la section **"Pipeline"** :

1. **Definition** : Sélectionnez **"Pipeline script from SCM"**

2. **SCM** : Sélectionnez **"Git"**

3. **Repository URL** :
```
   https://github.com/zoubamaryem/Jenkins-Demo.git
