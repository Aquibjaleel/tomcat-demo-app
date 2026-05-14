pipeline {
    agent any

    stages {

        stage('Deploy to Staging Environment') {
            steps {
                build job: 'deploy-application-staging-environment-pipeline'
            }
        }

        stage('Deploy to Production Environment') {
            steps {
                timeout(time: 5, unit: 'DAYS') {
                    input message: 'Approve PRODUCTION Deployment?'
                }

                build job: 'deploy-application-production-environment-pipeline'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }

            post {
                success {
                    archiveArtifacts artifacts: '**/*.war', fingerprint: true
                }
            }
        }
    }
} 
