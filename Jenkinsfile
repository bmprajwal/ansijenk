pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                // Checkout your GitHub repo with playbook and inventory
                git url: 'https://github.com/bmprajwal/ansijenk.git', branch: 'main'
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                withCredentials([sshUserPrivateKey(credentialsId: 'ec2-ssh-key', keyFileVariable: 'SSH_KEY')]) {
                    // Run ansible-playbook from the cloned repo directory using injected SSH key
                    sh '''
                       ansible-playbook -i inventory.yml playbook.yml --user ec2-user --private-key $SSH_KEY --become
                    '''
                }
            }
        }
    }
}
