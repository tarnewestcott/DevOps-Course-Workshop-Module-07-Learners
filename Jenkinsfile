pipeline {
    agent none

    stages {
        stage('Build nodejs') {

            agent {
                docker { image 'node:14-alpine' }
            }

            steps {
                echo 'Running npm install'
                sh "cd DotnetTemplate.Web && npm install"
            }

            stages {
                stage('Test') {
                    steps {
                        echo 'Running tests'
                        sh "cd DotnetTemplate.Web && npm run lint && npm run test"
                    }
                }
            }
        }
    }
}
