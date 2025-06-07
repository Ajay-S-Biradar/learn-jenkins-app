pipeline {
    agent {
        docker {
            image 'node:18-alpine'
            reuseNode true
        }
    }

    stages {
        stage('Build') {
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm i
                    npm run build
                    ls -la
                '''
            }
        }
        stage ("Test"){
            steps {
                sh '''test -f build/index.html
                    npm test'''
            }
        }
    }
    post {
        always {
            junit 'test-results/junit.xml'
        }
    }
}
