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
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }
        stage("Test") {
            steps {
                sh '''
                    test -f build/index.html
                    npm test
                    JEST_JUNIT_OUTPUT_DIR=test-results JEST_JUNIT_OUTPUT_NAME=junit.xml npx jest --reporters=default --reporters=jest-junit
                '''
            }
        }
    }

    post {
        always {
            junit 'test-results/junit.xml'
        }
    }
}
