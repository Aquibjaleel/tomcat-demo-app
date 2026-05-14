pipeline {
    agent any

    tools {
        maven 'maven'
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
                    tomcat9(
                        credentialsId: 'tomcat-credentials',
                        path: '',
                        url: 'http://20.228.110.132:8080'
                    )
                ],
                contextPath: 'tomcat-demo-app',
                war: 'target/tomcat-demo-app.war'
            }
        }
    }
}
