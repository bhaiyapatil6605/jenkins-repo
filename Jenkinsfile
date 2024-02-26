pipeline {
    agent any
    tools {
        git 'Default'
        maven 'maven'
        
    }
    stages {
        stage('Pull Git Codes') {
            steps {
                git 'https://github.com/bhaiyapatil6605/jenkins-repo.git'
            }
        }
        stage('Build with Maven') {
            steps {
                sh 'mvn clean install'
            }
        }
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
