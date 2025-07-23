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
            sh '''
               ssh-keyscan -H 172.31.2.180 >> ~/.ssh/known_hosts
               ssh-keyscan -H 172.31.9.118 >> ~/.ssh/known_hosts
               ansible-playbook -i inventory.yml playbook.yml --user ec2-user --private-key $SSH_KEY --become
            '''
        }
    }
}

    }
}
