pipeline {
    agent {
        docker {
            image 'artilleryio/artillery:1.7.7'
            args '-u root:root -i --entrypoint='
        }
    }

    triggers {
        cron('0 0 * * *')
    }

    stages {
        stage('Load Test') {
            steps {
                sh 'mkdir reports'
                sh '/home/node/artillery/bin/artillery run --output reports/report.json tests/performance/load-test.yaml'
                sh '/home/node/artillery/bin/artillery report --output reports/report.html reports/report.json'
            }
        }
    }

    post {
        success {
            archiveArtifacts 'reports/*'
        }
    }
}