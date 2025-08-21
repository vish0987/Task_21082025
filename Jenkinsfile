pipeline {
    agent any

    tools {
        maven 'Maven3'     // Make sure Maven is configured in Jenkins Global Tools
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/vish0987/Task_21082025.git', branch: 'main'
            }
        }

        stage('Build WAR with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy with Ansible') {
            steps {
                dir('ansible') { 
                        sh """
                        ansible-playbook -i inventory.ini playbook.yml -vvv
                        """
                    }
            }
        }
    }
}
