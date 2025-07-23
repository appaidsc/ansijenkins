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
                    // Run ansible-playbook from the cloned repo directory
                    sh '''
                       ansible-playbook -i inventory.yml playbook.yml --user ec2-user --become
                    '''
                }
            }
        }
    }
}
