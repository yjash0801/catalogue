pipeline {
    agent {
        node {
            label 'AGENT-1'
        }
    }
    environment {
        packageVersion = ''
        nexusURL = '172.31.38.156:8081'
    }
    options {
        timeout(time: 1, unit: 'HOURS')
        disableConcurrentBuilds()
    }
    parameters{
        booleanParam(name: 'Deploy', defaultValue: false, description: 'Toggle this value')
    }
    stages {
        stage('Get the version') {
            steps {
                script {
                    def packageJSON = readJSON file: 'package.json'
                    packageVersion = packageJSON.version
                    echo "application version: $packageVersion"
                }
            }
        }
    }
    post {
        always {
            echo 'I will always say Hello again!'
            deleteDir()
        }
        failure {
            echo 'This runs when pipeline is failed, used to send some alerts'
        }
        success {
            echo 'This runs when pipeline is success'
        }
    }
}
