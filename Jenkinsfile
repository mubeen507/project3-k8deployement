pipeline {
    agent any

    stages {
        stage('check out from SCM') {
            steps {
                git 'https://github.com/saikumarsagar/project1-docker.git'
            }
        }

    stage('MVN Build and Junit testing by MVN') {
            steps {
             sh 'mvn clean package'
              junit 'target/surefire-reports/*.xml'
            }
        } 
    stage('docker build') {
            steps {
             sh 'sudo docker build -t saidocker2048/project:1.0 .'
            }
        }
        
     stage('running docker container') {
            steps {
             sudo docker run -dt javacal -p 8090:8080 saidocker2048/project:1.0
            }
        }   
     stage('Pushing code to docker hub') {
            steps {
            withCredentials([string(credentialsId: '6636d3c5-1154-4ac0-8d3d-5f5649a671b7', variable: 'dockerpwd')])
            {
            sh "sudo docker login -u saidocker2048 -p ${dockerpwd}"
            sh 'sudo docker push saidocker2048/project:1.0'
            }
            }
        }  
        
          
    }
}
