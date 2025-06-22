pipeline {
    agent any
    tools {
        nodejs 'Node20'
    }

    options {
        skipDefaultCheckout(true)
    }

    stages {
        stage('Build') {
            steps {
                cleanWs()
                checkout scm
            }
        }
        stage('Test') {
            steps {
                sh '''
                    npm install
                    npm install -g newman
                '''
            }
        }
        stage('Run postman test with Newman') {
            steps {
               
               sh '''
                    npm run petstore-test
               '''
            }
        }
    }

    post {
        always {
            junit '**/report/junit-result.xml'
        }
        success {
            echo 'This will run only if the pipeline succeeds.'
        }
        failure {
            echo 'This will run only if the pipeline fails.'
        }
    }
}