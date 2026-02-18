pipeline {
    agent any

    stages {

        stage('Checkout Info') {
            steps {
                echo "Running Build ${BUILD_NUMBER}"
                sh 'pwd'
                sh 'ls -l'
            }
        }

        stage('Read File') {
            steps {
                sh 'cat app.txt'
            }
        }

        stage('Create Artifact') {
            steps {
                sh 'tar -cvf build.tar app.txt'
            }
        }
    }

    post {
        success {
            echo 'Build completed successfully'
        }
        failure {
            echo 'Build failed'
        }
    }
}

