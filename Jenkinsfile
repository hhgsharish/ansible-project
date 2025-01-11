pipeline {
    agent none

    stages {
        stage('Checkout') {
            agent any
            steps {
                // Checkout the Git repository containing the playbook and roles
                git url: 'https://github.com/your-org/ansible-project.git', branch: 'main'
            }
        }

        stage('Install Prometheus and Grafana on Node 1') {
            agent { label 'node-1' }  // Specify the label of the first Jenkins node
            steps {
                script {
                    // Run the Ansible playbook on Node 1
                    echo 'Installing Prometheus and Grafana on Node 1'
                    ansiblePlaybook playbook: 'prom_playbook.yml', inventory: 'inventory', credentialsId: 'ssh-credentials-id'
                }
            }
        }

        stage('Install Prometheus and Grafana on Node 2') {
            agent { label 'node-2' }  // Specify the label of the second Jenkins node
            steps {
                script {
                    // Run the Ansible playbook on Node 2
                    echo 'Installing Prometheus and Grafana on Node 2'
                    ansiblePlaybook playbook: 'prom_playbook.yml', inventory: 'inventory', credentialsId: 'ssh-credentials-id'
                }
            }
        }

        stage('Post-Installation Check') {
            agent any
            steps {
                script {
                    // Optional step to verify installation on both nodes
                    echo 'Post-installation checks for Prometheus and Grafana'
                }
            }
        }
    }

    post {
        always {
            echo 'Cleaning up and finishing the process.'
        }
        success {
            echo 'Prometheus and Grafana installed successfully on both nodes.'
        }
        failure {
            echo 'Installation failed. Check the logs for details.'
        }
    }
}
