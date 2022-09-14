pipeline {
    agent any
    environment {
        CI = true
        ARTIFACTORY_ACCESS_TOKEN = credentials('artifactory-access-token')
    }
    stages {
        
        stage ('Clone') {
            steps{
                
                git url: "https://github.com/frodriguezh/netcore.git", branch: "netcore"
            }
            
        }
        stage('Upload to Artifactory') {
          agent {
            docker {
              image 'releases-docker.jfrog.io/jfrog/jfrog-cli-v2:2.2.0' 
              reuseNode true
            }
          }
          steps {
            sh 'jfrog rt upload --url http://192.168.0.10:8082/artifactory/ --access-token ${ARTIFACTORY_ACCESS_TOKEN} core.sln result/'
          }
        }
    }
}
