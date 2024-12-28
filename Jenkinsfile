pipeline {
    agent any
    environment {
        BUN_VERSION = 'latest'
    }
    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/khaled-hamami/jenkins'
            }
        }
        stage('Setup Environment') {
            steps {
                script {
                    sh '''
                    curl -fsSL https://bun.sh/install | bash
                    export PATH="$HOME/.bun/bin:$PATH"
                    bun --version
                    '''
                }
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'bun install'
            }
        }
        stage('Build Application') {
            steps {
                sh 'bun run build'
            }
        }
        stage('Lint Application') {
            steps {
                sh 'bun run lint'
            }
        }
        stage('Start Application') {
            steps {
                sh 'bun run start'
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: '.next/**', allowEmptyArchive: true
        }
        success {
            echo 'Build and application ran successfully!'
        }
        failure {
            echo 'Build or deployment failed. Check the logs for details.'
        }
    }
}
