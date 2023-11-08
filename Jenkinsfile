pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                script {
                    checkout([$class: 'GitSCM', branches: [[name: '*/master']],
                     doGenerateSubmoduleConfigurations: false, extensions: [], 
                     userRemoteConfigs: [[url: 'https://github.com/SnehashisWalk/jenkins-terraform-react']]])
                }
            }
        }

        stage('Build and Test') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }

        stage('Deploy') {
            steps {
                sh 'aws s3 sync build/ s3://web-app-jenkins-terraform/'

                sh 'aws s3 website s3://your-s3-bucket-name/ --index-document index.html --error-document index.html'
            }
        }
    }
}
