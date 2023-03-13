def COLOR_MAP = [
    'SUCCESS': 'good', 
    'FAILURE': 'danger',
]
pipeline {
    agent any
    
    environment {
        registryCredential = 'ecr:us-east-1:awscreds'
        appRegistry = '334671708617.dkr.ecr.us-east-1.amazonaws.com/aws-ecr-java-app'
        awsRegistry = "https://334671708617.dkr.ecr.us-east-1.amazonaws.com"
        cluster = "Stagging-Environment"
        service = "java-app-service"
    }

    stages {
        stage('Build App Image') {
            steps {
                script {
                    dockerImage = docker.build( appRegistry + ":$BUILD_NUMBER", "./Dockerfiles/App/")
                }
            }
        }
        
        stage('Upload App Image') {
          steps{
            script {
              docker.withRegistry( awsRegistry, registryCredential ) {
                dockerImage.push("$BUILD_NUMBER")
                dockerImage.push('latest')
              }
            }
          }
        }
        
    }
}
