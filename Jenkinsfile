pipeline {
    agent none

    stages {
        stage('Build nodejs') {

            agent {
                docker { image 'node:14-alpine' }
            }

            steps {
                echo 'Running npm install'
                cd DotnetTemplate.Web
                npm install
            }

            stages {
                stage('Test') {
                    steps {
                        echo 'Running tests'
                        cd DotnetTemplate.Web
                        npm run lint
                        npm run test
                    }
                }
            }
        }
    }
}
