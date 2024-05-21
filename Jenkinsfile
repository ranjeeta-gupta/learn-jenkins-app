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
        stage('Unit test') {
            agent {
              docker {
                    image 'node:18-alpine'
                    reuseNode true
                   }
            }
           steps {
             echo ' Unit Testing the Application'
             sh '''
             test -f build/index.html
             npm test
             '''
           }
        }

          stage('E2E') {
            agent {
              docker {
                    image 'mcr.microsoft.com/playwright:v1.44.0-jammy'
                    reuseNode true
                   }
            }
           steps {
             echo ' E2E Application Testing'
             sh '''
             npm install serve 
             node_modules/.bin/serve -s build
             npx playwright test
             '''
           }
        }
    }


    post {
      always {
        junit 'jest-results/junit.xml'
      }
    }
}
