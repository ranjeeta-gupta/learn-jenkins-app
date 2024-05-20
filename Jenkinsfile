pipeline {
   
agent any 
    stages {
        stage('Build') {
             agent {
              docker {
                    image 'node:20.11.1-alpine3.19'
                    reuseNode true
              }
            }
            steps {
                echo 'Building the application'
                sh '''
                node --version
                npm --version
                ls -la
                npm ci
                npm run build 
                ls -la
                '''
            }
        }
        stage('test') {
            agent {
              docker {
                    image 'node:20.11.1-alpine3.19'
                    reuseNode true
                   }
            }
           steps {
             echo ' testing the application'
             sh '''
             test -f build/index.html
             npm test
             '''
           }
        }
    }
}
