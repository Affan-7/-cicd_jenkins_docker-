node{
     
    stage('Clonnig the code from github'){
        git url: 'https://github.com/Affan-7/-cicd_jenkins_docker-.git',branch: 'master'
    }
    
    stage("Compiling the code"){
      sh "mvn clean package"
      
    } 
    
    
    stage('Building Docker Image'){
        sh 'docker build -t affan7/web_app .'
    }

    stage('Deleting existing container'){
        sh 'docker stop java-web-app || true && docker rm java-web-app || true'
    }
    
    stage('Pushing Docker Image'){
        withCredentials([string(credentialsId: 'docker_hub_password', variable: 'docker_hub_password')]) {
          sh "docker login -u affan7 -p ${docker_hub_password}"
        }
        sh 'docker push affan7/web_app'
     }
     
      stage('Deploying docker image'){
        sh "docker run -d -p 80:8080 --name java-web-app affan7/web_app"
       }
       
    }
     

