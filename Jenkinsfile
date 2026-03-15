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

        stage('Deploy via Ansible (Secure)') {
            steps {
                withCredentials([
                    sshUserPrivateKey(
                        credentialsId: 'ansible-ssh-key',
                        keyFileVariable: 'SSH_KEY',
                        usernameVariable: 'SSH_USER'
                    )
                ]) {
                    sh '''
                        export ANSIBLE_PRIVATE_KEY_FILE=$SSH_KEY
                        cp build.tar /opt/ansible/
                        cd /opt/ansible
                        ansible-playbook -i /opt/ansible/inventory/hosts /opt/ansible/playbooks/deploy.yml \
                          -u $SSH_USER
                    '''
                }
            }
        }
    }
}

