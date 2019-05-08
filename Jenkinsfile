pipeline{
    agent any
    stages{
        stage('Pull Latest Image'){
            steps{
                sh "docker pull 192.168.0.3:5000/sdt/pega-automated-tests"
            }
        }
        stage('Start Grid'){
            steps{
                sh "docker-compose up -d hub chrome firefox"
            }
        }
        stage('Run Test'){
            steps{
                sh 'docker-compose up OnlineReporting-chrome OnlineReporting-firefox'
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