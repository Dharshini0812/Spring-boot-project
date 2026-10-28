
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Dharshini0812/Spring-boot-project.git'
            }
        }

        stage('Check Tools') {
            steps {
                sh 'java -version'
                sh 'mvn -version'
            }
        }

        stage('Build Maven Project') {
            steps {
                sh 'mvn clean package'
            }
        }
    }

    post {
        success {
            echo 'Maven project built successfully!'
        }
        failure {
            echo 'Build failed. Check Console Output.'
        }
    }
}
