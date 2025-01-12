pipeline {
    agent any

    stages {
        stage('git clone') {
            steps {
              git 'https://github.com/Herchelle24/java-azure-project.git'
            }
        }
        stage('build') {
            steps {
              sh "mvn clean package"
            }
        }
        stage('Build Docker OWN image') {
            steps {
                sh "sudo docker build -t herchellee/javasanta24:latest ."

            }
        }
        stage('docker push ') {
            steps {
                withCredentials([string(credentialsId: 'DOCKER_HUB_PWD', variable: 'DOCKER_HUB_PASSCODE')]) {
    // some block
                sh "sudo docker login -u herchellee -p $DOCKER_HUB_PASSCODE"
                    }
                sh "sudo docker push herchellee/javasanta24:latest"
                }
            } 
        stage('Deploy to docker Env') {
            steps {
                sh "sudo docker rm -f app3" 
                sh "sudo docker run -itd --name app3 -p 9000:8080 herchellee/javasanta24:latest" 

                }
        }
    }
}
