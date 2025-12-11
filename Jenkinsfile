pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // 깃 클론 (이미 Pipeline from SCM 쓰면 Jenkins가 자동으로 함, 그땐 이 stage 빼도 됨)
                git url: 'https://github.com/excelh11/jenkins-deploy', branch: 'master'
            }
        }

        stage('Build') {
            steps {
                sh '''
                    echo "=== Build 시작 ==="
                    chmod +x gradlew
                    ./gradlew clean build
                '''
            }
        }

        stage('Deploy') {
            steps {
                script {
                    sshagent(credentials: ['root']) {
                        sh '''
                            echo "=== JAR 파일 서버로 전송 ==="
                            scp -o StrictHostKeyChecking=no build/libs/shortenurlservice-0.0.1-SNAPSHOT.jar root@141.164.46.243:/root/

                            echo "=== 원격 서버에서 deploy.sh 실행 ==="
                            ssh -o StrictHostKeyChecking=no root@141.164.46.243 /root/deploy.sh
                        '''
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment success.'
        }
        failure {
            echo 'Deployment failed.'
        }
    }
}
