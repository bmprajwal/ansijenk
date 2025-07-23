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
        sshagent(credentials: ['ec2-ssh-key']) {
            sh '''
               mkdir -p ~/.ssh
               ssh-keyscan -H 172.31.2.180 >> ~/.ssh/known_hosts
               ssh-keyscan -H 172.31.9.118 >> ~/.ssh/known_hosts
               ssh-keyscan -H 172.31.4.171 >> ~/.ssh/known_hosts

               ansible-playbook -i inventory.yml playbook.yml --user ec2-user --become
            '''
        }
    }
}

    }
}
