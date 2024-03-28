pipeline {
    agent any  // Use any available agent

    stages {
        stage('Clone repository') {
            steps {
                node {  // Run this stage on any available agent
                    checkout scm
                }
            }
        }
        stage('Build image') {
            steps {
                node {  // Run this stage on any available agent
                    script {
                        def app = docker.build("mjovanovik/kiii-jenkins")
                    }
                }
            }
        }
        stage('Push image') {
            steps {
                node {  // Run this stage on any available agent
                    script {
                        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                            app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                            app.push("${env.BRANCH_NAME}-latest")
                        }
                    }
                }
            }
        }
    }
}
