pipeline {
    agent any
    environment {
        ANSIBLE_USER = 'poovarasan'  // Replace with your Ansible server user
        ANSIBLE_HOST = '172.19.81.222' // Replace with your Ansible server IP
    }
    stages {
        stage('Checkout') {
            steps {
                // Checkout the latest changes from GitHub
                git branch: 'main', url: 'https://github.com/flowerking146/ansible_playbooks_test.git'
            }
        }
        stage('Test YAML') {
            steps {
                // Example: Running Ansible playbook to test the YAML file
                script {
                    sh 'ansible-playbook -i /etc/ansible/hosts /etc/ansible/playbooks/'
                }
            }
        }
        stage('Update Ansible Server') {
            steps {
                // Copy the updated YAML file to the Ansible server
                script {
                    sshagent(credentials: ['your-ssh-credentials-id']) {
                        sh 'scp ${WORKSPACE}/your_yml_file.yml poovarasan@172.19.81.222:/etc/ansible/playbooks/'
                    }
                }
            }
        }
    }
    post {
        success {
            echo 'YAML file has been updated successfully!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
