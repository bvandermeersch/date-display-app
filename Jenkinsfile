node() {
    echo "Your Pipeline works!"
    def commitHash = checkout(scm).GIT_COMMIT    
    sh('ls')

    pipeline {
    agent {
        docker { image 'node:7-alpine' }
    }
    stages {
        stage('Test') {
            steps {
                sh 'node --version'
            }
        }
    }
}
}
