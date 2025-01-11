pipeline {
    agent { label 'slave' }

    environment {
        ANSIBLE_HOST_KEY_CHECKING = 'False' // Disable host key checking if needed
    }

    stages {
        stage('Clone Repository') {
            steps {
                // Checkout the code from GitHub
                git branch: 'main', url: 'https://github.com/hhgsharish/ansible-project.git'
            }
        }
        
        stage('Run Ansible Playbook') {
            steps {
                // Install Ansible (optional if it’s not installed globally)
                sh 'sudo apt update && sudo apt install -y ansible'

                // Run the Ansible playbook
                sh 'ansible-playbook -i inventory prom_playbook.yml'
            }
        }
    }
}
