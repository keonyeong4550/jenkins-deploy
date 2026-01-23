pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                sh 'chmod +x gradlew'
                sh './gradlew clean build'
            }
        }

        stage('Deploy') {
            steps {
                script {
                    def jarFile   = 'build/libs/shortenurlservice-0.0.1-SNAPSHOT.jar'
                    def serverIp  = '52.79.95.30' // application-instance-1 공개주소
                    def deployDir = '/root'

                    sshagent(['deploy_ssh_key']) {
                        sh "scp -o StrictHostKeyChecking=no ${jarFile} root@${serverIp}:${deployDir}/"
                        sh "ssh -o StrictHostKeyChecking=no root@${serverIp} '/root/deploy.sh'"
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment was successful.'
        }
        failure {
            echo 'Deployment failed.'
        }
    }
}
