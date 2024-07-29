pipeline {
    agent {
        node {
            label 'AGENT-1'
        }
    }
    environment { 
        packageVersion = ''
    }
    options {
        // Timeout counter starts AFTER agent is allocated
        timeout(time: 1, unit: 'HOURS')
        disableConcurrentBuilds()
        ansiColor('xterm')
    }
    // parameters {
    //     string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')

    //     text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')

    //     booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')

    //     choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')

    //     password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    // }
    // build
    stages {
        stage('Get the version') {
            steps {
                script{
                    def packageJSON = readJSON file: 'package.json'
                    packageVersion = packageJSON.version
                    echo "application version: $packageVersion"
                }
            }
        }
       stage('Install the dependencies') {
            steps {
                sh """
                npm install
                """
            }
        }
        stage('Build') {
            steps {
                sh """
                    ls -la
                    #rm -f catalogue.zip
                    zip -q -r catalogue.zip ./* -x ".git" -x "*.zip"
                    ls -ltr
                """
            }
        }
    }
    // post build
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