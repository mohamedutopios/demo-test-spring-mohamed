pipeline {
    agent any
    tools {
        maven 'maven'
    }

    stages {
        stage('Run Test') {
            steps {
                bat 'mvn test'
            }

            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }

        stage('Sonar Analyse') {
            steps {
                script {
                    withSonarQubeEnv(installationName: 'sonar', credentialsId: 'jenkins-sonar-token') {
                        bat 'mvn sonar:sonar'
                    }
                }
            }
        }
        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }
    }
}
