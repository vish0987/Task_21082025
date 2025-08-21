pipeline {
    agent any

    tools {
        maven 'Maven3'     // Make sure Maven is configured in Jenkins Global Tools
    }

    environment {
        SONAR_TOKEN = credentials('sonar-token') // Jenkins secret text credentials
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

        stage('SonarQube Analysis') {
            steps {
                    withSonarQubeEnv('sonarqube') {
                        sh 'mvn sonar:sonar -Dsonar.projectKey=devops_git'
                }
            }
        }

        stage('Check Quality Gate') {
            steps {
                sh '''
                curl -s -u $SONAR_TOKEN: \
                'http://localhost:9000/api/qualitygates/project_status?projectKey=devops_login' \
                | grep -q '"status":"ERROR"' && echo 'Quality Gate FAILED' && exit 1 || echo 'Quality Gate PASSED'
                '''
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
