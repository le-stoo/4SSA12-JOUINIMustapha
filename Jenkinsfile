pipeline {
    agent any

    options {
        skipDefaultCheckout()
    }

    tools {
        jdk   'JAVA_HOME'
        maven 'M2_HOME'
    }

    stages {

        stage('Récupération du code') {
            steps {
                checkout scm
                sh 'git log -1 --oneline'
                sh 'ls -la'
            }
        }

        stage('Création du livrable') {
            steps {
                dir('backend') {
                    sh 'mvn clean package -DskipTests'
                }
            }
            post {
                success {
                    archiveArtifacts artifacts: 'backend/target/*.jar', fingerprint: true
                }
            }
        }
    }
}
