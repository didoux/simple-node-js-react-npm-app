pipeline {
   agent {
       docker {
           image 'node:latest'
           args '-v $HOME/.npm:/root/.npm'
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
                sh 'hostname'
                sh 'ls -lta'
                sh 'ls -lta /'
                sh 'df -h'
                //sh 'mkdir /.npm'
                sh 'npm -g config set user root'
		sh 'node --version'
		sh 'npm --version'
                sh 'npm install'
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
