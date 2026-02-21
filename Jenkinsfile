pipeline {
    agent any

    environment {
        DEPLOY_USER = "ec2-user"
        DEPLOY_HOST = "47.130.155.189"
        DEPLOY_DIR  = "/opt/app"
    }

    stages {

        stage('Quality Check') {
            steps {
                sh '''
                    if [ ! -f app.txt ]; then
                        echo "ERROR: app.txt not found"
                        exit 1
                    fi
                '''
            }
        }

        stage('Build Artifact') {
            steps {
                sh 'tar -cvf build.tar app.txt'
            }
        }

        stage('Deploy to Server') {
            steps {
                sh '''
                    echo "Deploying to server..."
                    scp build.tar ${DEPLOY_USER}@${DEPLOY_HOST}:${DEPLOY_DIR}
                    ssh ${DEPLOY_USER}@${DEPLOY_HOST} "
                        cd ${DEPLOY_DIR} &&
                        tar -xvf build.tar
                    "
                '''
            }
        }
    }

    post {
        success {
            echo 'CD SUCCESS – Application deployed'
        }
        failure {
            echo 'CD FAILED – Deployment aborted'
        }
    }
}

