pipeline {
    agent any


    stages {
        stage('Checkout') {
            steps {
                    git branch: 'main',
                        url: 'https://github.com/sunil338/QA_tasks.git'
            }
        }

        stage('Build') {
            steps {
                    sh 'mvn clean install'
            }
        }

       
        stage('Deploy to Tomcat') {
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
