pipeline {
    agent any
    tools {
        git tool: 'Default', name: 'git'
        maven name: 'maven'
        msBuild name: 'SonarScannermsvuild'
        sonarqube name: 'sonarqube_scaner'
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
                    sh '''mvn clean verify sonar:sonar 
                        -Dsonar.projectKey=demo 
                        -Dsonar.host.url=http://localhost:32768 
                        -Dsonar.login=sqp_557cad7383597fa1f537d12188539e11203deefa'''
                }
            }
        }
        stage('Deploy on Tomcat') {
            steps {
                script {
                    sh 'cp -r /var/lib/jenkins/workspace/ci-job/target/*.war /opt/apache-tomcat-8.5.99/webapps/'
                    //copy
                }
            }
        }
    }
}
