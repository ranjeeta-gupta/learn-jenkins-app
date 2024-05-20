pipeline {
   
agent any 
 environment {
        npm_config_cache = 'npm-cache'
    }
    stages {
        stage('Build') {
             agent {
              docker {
                    image 'node:18-alpine'
                    reuseNode true
              }
            }
            steps {
                echo 'Building the application'
                sh '''
                node --version
                npm --version
                ls -la
                npm install
                npm run build 
                ls -la
                '''
            }
        }
        stage('test') {
            agent {
              docker {
                    image 'node:18-alpine'
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
