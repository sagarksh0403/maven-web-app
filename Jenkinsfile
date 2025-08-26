pipeline {
    agent any

    tools {
        maven 'maven-1' // Make sure this matches your Jenkins Maven installation name
    }

    environment {
        MAVEN_OPTS = "-Dmaven.repo.local=.m2/repository"
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/sagarksh0403/maven-web-app.git'
            }
        }

        stage('Build & Deploy to Nexus') {
            steps {
                bat 'mvn clean deploy -s "C:\\ProgramData\\Jenkins\\.jenkins\\.m2\\settings.xml"'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                bat '''
scp -v -o StrictHostKeyChecking=no ^
    -i C:\\Users\\Sagar\\Downloads\\pemkey.pem ^
    target\\maven-web-app.war ^
    ec2-user@35.154.21.129:/opt/apache-tomcat-9.0.107/webapps/
'''
            }
        }
    }
}
