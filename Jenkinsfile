pipeline{
    agent any
    tools{
        maven 'maven3'
    }
    stages{
        stage("clone"){
            steps{
                git branch: 'main', credentialsId: 'git-cred', url: 'https://github.com/assumptagithub/wordsmith-api.git'
                sh"ls -l" 
            }
        }
        stage("Maven test"){
            steps{
                sh"mvn test"
            }
        }
        stage("Maven pakages"){
            steps{
                sh"mvn clean package"
                sh"ls -l target/"
            }
        }
        stage('Docker Build Push'){
            steps{
                script{
                  withDockerRegistry(credentialsId: 'dockerhub_cred') {
                      sh"docker build -t munjo185/munjo-app:latest ."
                      sh"docker push munjo185/munjo-app:latest" 
                    }  
                }
            }
        }
    }
}
