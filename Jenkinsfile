pipeline {
    agent any
    
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
                    withCredentials([string(credentialsId: 'sonarqube', variable: 'sonarqube')]) {
                        sh 'mvn clean verify sonar:sonar \
                        -Dsonar.projectKey=demo \
                        -Dsonar.host.url=http://localhost:32768'
                    }
                }
            }
        }
        stage('Deploy on Tomcat') {
            steps {
                script {
                    sh 'cp -r /var/lib/jenkins/workspace/ci-job/target /opt/apache-tomcat-8.5.99/webapps/'
                }
            }
        }
    }
}
