
pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Dharshini0812/Spring-boot-project.git'
            }
        }

        stage('Check Java and Maven') {
            steps {
                sh 'java -version'
                sh 'mvn -version'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    set -eu

                    JAR_FILE=$(find target -maxdepth 1 \
                        -type f -name "*.jar" \
                        ! -name "*-sources.jar" \
                        ! -name "*-javadoc.jar" | head -n 1)

                    test -n "$JAR_FILE"

                    sudo mkdir -p /opt/springboot-app
                    sudo cp "$JAR_FILE" /opt/springboot-app/app.jar
                    sudo systemctl restart springboot-app
                    sudo systemctl is-active --quiet springboot-app
                '''
            }
        }
    }

    post {
        success {
            echo 'Build and deployment completed successfully!'
        }
        failure {
            echo 'Build or deployment failed. Check Console Output.'
        }
    }
}
