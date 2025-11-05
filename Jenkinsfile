pipeline 

    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/alsayedhany/jenkins-web-demo.git'
           }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t jenkins-web-demo .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                docker rm -f jenkins-web-demo || true
                docker run -d -p 3000:3000 --name jenkins-web-demo jenkins-web-demo
                '''
            }
        }
       stage('Test Application') {
             steps {
                 sh '''
                     for i in {1..5}; do
                      curl -f http://localhost:3000 && exit 0
                     echo "Waiting for app to start..."
                     sleep 2
                     done
                      echo "App did not start in time"
                     exit 1
                 '''
        }
    }
}