pipeline {
    agent none

    stages {
        parallel {
            stage('Build nodejs') {

                agent {
                    docker { image 'node:14-alpine' }
                }

                stages {
                    stage('Install'){
                        steps {
                            echo 'Running npm install'
                            sh "cd DotnetTemplate.Web && npm install"
                        }
                    }
                    stage('Test') {
                        steps {
                            echo 'Running tests'
                            sh "cd DotnetTemplate.Web && npm run lint && npm run test"
                        }
                    }
                }
            }

            stage('Build .Net') {

                environment {
                    DOTNET_CLI_HOME = "/tmp/DOTNET_CLI_HOME"
                }

                agent {
                    docker { image 'mcr.microsoft.com/dotnet/sdk:5.0' }
                }

                stages {
                    stage('Install'){
                        steps {
                            echo 'Running build'
                            sh "dotnet build"
                        }
                    }
                    stage('Test') {
                        steps {
                            echo 'Running tests'
                            sh "dotnet test"
                        }
                    }
                }
            }
        }
    }
}
