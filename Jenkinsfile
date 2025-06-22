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
            junit {
                testResults '/**/report/junit-result.xml'
                // Assuming the Newman test results are in a specific format
                // Adjust the path according to your project structure
                allowEmptyResults(true)
            }
        }
        success {
            echo 'This will run only if the pipeline succeeds.'
        }
        failure {
            echo 'This will run only if the pipeline fails.'
        }
    }
}