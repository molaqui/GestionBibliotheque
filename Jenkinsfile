pipeline {
    agent any
    environment {
    MAVEN_HOME= tool 'Maven'
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/molaqui/GestionBibliotheque.git'
            }
        }
        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }
        stage('Quality Analysis') {
            steps {
                withSonarQubeEnv('sonar') {
                    bat 'mvn sonar:sonar'
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Déploiement simulé réussi'
            }
        }
    }
    post {
        success {
            emailext ( to: 'abdrahimmolaqui@gmail.com',
                subject: 'Build Success',
                body: 'Le build a été complété avec succès.')
        }
        failure {
            emailext ( to: 'abdrahimmolaqui@gmail.com',
                subject: 'Build Failed',
                body: 'Le build a échoué.')
        }
    }
}
