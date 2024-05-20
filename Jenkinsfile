pipeline {
    agent any 
      docker {
                    image 'node:18-alpine'
                    reuseNode true
            }

    stages {
        stage('Build') {
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
           steps {
             echo ' testing the application'
             sh '''
             test -f 'build/index.html
             npm test
             '''
           }
        }
    }
}
