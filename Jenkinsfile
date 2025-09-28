pipeline{
    agent any // the current machine where we have to run the pipeline 
    tools{
        maven 'mymaven'
    }
    stages{
        stage('Checkout Code'){
            steps{
                git 'https://github.com/Sonal0409/DevOpsCodeDemo.git'
            }
        }
        stage('Compile Code'){
            steps{
                sh 'mvn compile'
            }
        }
        stage('Test code'){
            steps{
                sh 'mvn test'
            }
        }
        stage('package code'){
            steps{
                sh 'mvn package'
            }
        }
        stage('Build Image'){
            steps{
                sh 'docker build -t myaddressbook .'
            }

        }
        stage('push image to dockerhub'){
            steps{
               withCredentials([string(credentialsId: 'DOCKER_HUB_PASWD', variable: 'DOCKER_HUB_PASSWD')]) {
                 sh 'docker login -u sonal04 -p ${DOCKER_HUB_PASSWD}'
}               
                sh 'docker tag myaddressbook sonal04/myaddressbook'
                sh 'docker push sonal04/myaddressbook'
            }
        }
        stage('Deploy the container'){
            steps{
                sh 'docker run -d -P sonal04/myaddressbook'
            }
        }
    }

}
