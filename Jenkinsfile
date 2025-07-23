pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                // Checkout your GitHub repo with playbook and inventory
                git url: 'https://github.com/appaidsc/ansijenkins.git', branch: 'main'
            }
        }

        stage('Run Ansible Playbook') {
    steps {
        sshagent(credentials: ['ec2-ssh-key']) {
            sh '''
               mkdir -p ~/.ssh
               ssh-keyscan -H 172.31.16.51 >> ~/.ssh/known_hosts
               ssh-keyscan -H 172.31.23.6 >> ~/.ssh/known_hosts
               ssh-keyscan -H 172.31.28.51 >> ~/.ssh/known_hosts

               ansible-playbook -i inventory.yml playbook.yml --user ec2-user --become
            '''
        }
    }
}

    }
}
