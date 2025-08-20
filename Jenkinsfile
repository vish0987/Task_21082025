pipeline {
    agent any

    tools {
        maven 'Maven3'     // Make sure Maven is configured in Jenkins Global Tools
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/sunil338/QA_tasks.git', branch: 'main'
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
