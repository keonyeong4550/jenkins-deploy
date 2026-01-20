

# Jenkins CICD deploy
## putty 에서 
### 1. 리눅스 업데이트
sudo dnf update -y

### 2. 도커 설치
sudo dnf install dnf-plugins-core -y
sudo dnf config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
sudo dnf install docker-ce docker-ce-cli containerd.io -y

### 3. 도커 서비스 시작
sudo systemctl start docker
sudo systemctl enable docker

### 4. 젠킨스 도커 이미지 Pull,  컨테이너 시작
sudo docker run -d -p 8080:8080 -p 50000:50000 --name jenkins --restart=always -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts

### 5. 초기 비밀번호 보기
sudo docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword

![젠킨스 배포 흐름도](https://github.com/user-attachments/assets/7a9ad296-fbbd-4b27-912f-61adc8c6507c)



#### 참고 출처: [애플리케이션 배포 자동화와 CI/CD](https://www.inflearn.com/course/%EC%95%A0%ED%94%8C%EB%A6%AC%EC%BC%80%EC%9D%B4%EC%85%98-%EB%B0%B0%ED%8F%AC-%EC%9E%90%EB%8F%99%ED%99%94-ci-cd)

