pipeline {
    agent {
        docker {
            image 'node:16-bullseye-slim'
            args '-v /var/jenkins_home/workspace/react-jenkins/build:/var/jenkins_home/workspace/react-jenkins/build'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
                input message: "Continue?"
            }
        }
        stage('Deploy') {
            steps {
                inside {
                    sshagent(credentials: ['333f59a6-a684-4ae2-a880-7e2b0d8ee21d']) {
                        sh 'ssh user@server "mkdir -p /var/www/html/my-app"'
                        sh 'scp -r build/* user@server:/var/www/html/my-app'
                    }
                }
            }
        }
    }
}
