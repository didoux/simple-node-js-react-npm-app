pipeline {
   agent {
       docker {
           image 'node:latest'
           args '-v /root/.npm:/root/.npm'
           args '-p 3000:3000'
        }
    }
    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
                sh 'uname -a'
                sh 'ls -lta'
                sh 'ls -lta /'
                sh 'df -h'
                sh 'mkdir /.npm'
                sh 'sudo npm install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}
