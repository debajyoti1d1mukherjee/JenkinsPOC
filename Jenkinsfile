pipeline {
    environment{
        envVar1 = "environment variable1"
        envVar2 = "environment variable2"
        envVar3 = "environment variable3"
    }
    agent any
    tools {
        maven 'jenkins-maven'
        dockerTool 'jenkins-docker'
    }
    stages {
        stage('Git Checkout') { 
            steps {
                sh 'echo ${envVar1}'
                echo "${env.BRANCH_NAME}"
                sh '''
                  rm -rf *
                  git clone https://github.com/debajyoti1d1mukherjee/KubernetesPlatformServices.git
                '''
            }
        }    
        stage('Maven Build') { 
            steps {
                sh '''
                  cd KubernetesPlatformServices/serviceregistry
                  mvn clean install -Dmaven.test.skip
                '''
            }    
        }
        stage('Docker Build') { 
            steps {
                sh '''
                  cd KubernetesPlatformServices/serviceregistry/src/main/docker
                  docker build -t debajyotim/serviceregistry .
                '''
            }    
        }

    }
}