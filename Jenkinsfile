pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build WAR') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                deploy adapters: [
                    tomcat10(
                        credentialsId: 'tomcat-credentials',
                        path: '',
                        url: 'http://20.98.164.215:8080'
                    )
                ],
                contextPath: 'tomcat-demo-app',
                war: 'target/tomcat-demo-app.war'
            }
        }
    }
}