pipeline {
    agent any 
    
  
    
   
    
    stages{
        
        stage("Git Checkout"){
            steps{
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/jaiswaladi246/Petclinic.git'
            }
        }
        
        stage("Compile"){
            steps{
                sh "mvn clean compile"
            }
        }
        
         stage("Test Cases"){
            steps{
                sh "mvn test"
            }
        }
        
      
        
        
        
         stage("Build"){
            steps{
                sh " mvn clean install"
            }
        }
        
        stage("Docker Build & Push"){
            steps{
                script{
                   withDockerRegistry(credentialsId: '58be877c-9294-410e-98ee-6a959d73b352', toolName: 'docker') {
                        
                        sh "docker build -t image1 ."
                        sh "docker tag image1 adijaiswal/pet-clinic123:latest "
                        sh "docker push adijaiswal/pet-clinic123:latest "
                    }
                }
            }
        }
        
        stage("TRIVY"){
            steps{
                sh " trivy image adijaiswal/pet-clinic123:latest"
            }
        }
        
    }
}
