pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                sh 'pwd'
                sh 'ls -l'
            }
        }

        stage('Quality Check') {
            steps {
                sh '''
                    echo "Running quality checks..."

                    if [ ! -f app.txt ]; then
                        echo "ERROR: app.txt not found"
                        exit 1
                    fi

                    echo "Quality check passed"
                '''
            }
        }

        stage('Build Artifact') {
            steps {
                sh 'tar -cvf build.tar app.txt'
            }
        }
    }

    post {
        success {
            echo 'CI Pipeline SUCCESS'
        }
        failure {
            echo 'CI Pipeline FAILED'
        }
    }
}

