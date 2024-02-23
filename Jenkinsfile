pipeline {
    agent any
    tools {
        git 'Default'
        maven 'maven'
        
    }
    stages {
        stage('Pull Git Codes') {
            steps {
                git 'https://github.com/deepak-umre/jenkins_ci.git'
            }
        }
        stage('Build with Maven') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Test on SonarQube') {
            steps {
                script {
                    sh '''mvn clean verify sonar:sonar \
                    -Dsonar.projectKey=demo \
                    -Dsonar.host.url=http://localhost:9000 \
                    -Dsonar.login=sqp_46489272405d97111af92c42c1324a64ab9f6d3b'''
                }
            }
        }
        stage('Deploy on Tomcat') {
            steps {
                script {
                    sh 'cp -r /var/lib/jenkins/workspace/demo/target/*.war /opt/apache-tomcat-8.5.99/webapps/'
                    //copy
                }
            }
        }
    }
}
