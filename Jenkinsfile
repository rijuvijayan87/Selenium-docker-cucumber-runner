pipeline{
    agent any
    stages{
        stage('Pull Latest Image'){
            steps{
                sh "docker pull 192.168.0.3:5000/rijuvijayan/selenium-docker-cucumber"
            }
        }
        stage('Start Grid'){
            steps{
                sh "docker-compose up -d hub chrome firefox"
            }
        }
        stage('Run Test'){
            steps{
                sh 'docker-compose up registration-module-chrome registration-module-firefox'
            }
        }
    }
    post{
        always{
            archiveArtifacts artifacts: 'test-results/**'
            sh "docker-compose down"
        }
    }
}