pipeline{
    agent any
    stages{
        stage('Pull Latest Image'){
            steps{
                sh "docker pull 10.0.3.5:5000/sdt/pega-automated-tests"
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
        stage('Cucumber Reports'){
            steps{
                cucumber buildStatus: "UNSTABLE",
                fileIncludePattern: "**/cucumber.json",
                jsonReportDirectory: 'target'
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
