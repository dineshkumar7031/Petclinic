pipeline {
    agent any 
   
    
    stages{
        
        stage("Git Checkout"){
            steps{
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/dineshkumar7031/Petclinic.git'
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
        stage("sonar check"){
            steps{
                script{
                withSonarQubeEnv(credentialsId: 'sonar') {
                    sh "mvn sonar:sonar"
                }
            }
            }
        }
        stage("Docker Build & Push"){
            steps{
                script{
                   withDockerRegistry(credentialsId: 'dinesh9849', toolName: 'docker') { 
                        
                        sh "docker build -t image1 ."
                        sh "docker tag image1 dinesh9849/pet-clinic123:latest "
                        sh "docker push dinesh9849/pet-clinic123:latest "
                    }
                }
            }
        }
        
        stage("TRIVY"){
            steps{
                sh " trivy image dinesh9849/pet-clinic123:latest"
            }
        }
        
    }
}
