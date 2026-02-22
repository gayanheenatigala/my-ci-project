pipeline {
    agent any

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

        stage('Deploy via Ansible') {
            steps {
                sh '''
                    cp build.tar /opt/ansible/
                    cd /opt/ansible
                    ansible-playbook -i inventory/hosts playbooks/deploy.yml
                '''
            }
        }
    }

    post {
        success {
            echo 'Deployment completed via Ansible'
        }
        failure {
            echo 'Deployment failed'
        }
    }
}

