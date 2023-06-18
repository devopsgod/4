pipeline {
    agent any
    stages {
        stage('Clone repository') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], 
                doGenerateSubmoduleConfigurations: false, 
                extensions: [], submoduleCfg: [], 
                userRemoteConfigs: [[url: 'https://github.com/devopsgod/4']]])
            }
        }
        stage('Build image') {
            steps {
                script {
                    // Build Docker image
                    def dockerfile = readFile('Dockerfile')
                    def app = docker.build("myapp", "- < ${dockerfile}")
                }
            }
        }
        stage('Test image') {
            steps {
                script {
                    // Run the Docker container
                    def app = docker.image('myapp')
                    app.inside("-p 8000:8000") {
                        sh 'gradle test'
                    }
                }
            }
        }
        stage('Deploy image') {
            steps {
                script {
                    def app = docker.image('myapp')
                    docker.withRun("-p 8000:8000 ${app.id}") {
                        sh 'echo "App is running"'
                    }
                }
            }
        }
    }
}
