pipeline {
    agent any

    environment {
        APP_ENV = 'development'
    }

    stages{
        stage('Checkout') {
            steps{
                git branch: 'develop',
                url: 'https://github.com/vimal-iotasol/test-jenkins.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    // Install composer dependencies
                    sh 'composer install --prefer-dist --no-ansi --no-interaction --no-progress --no-scripts --optimize-autoloader'
                }
            }
        }
    }

    post {
        always {
            sh 'git fetch'

            sh 'git checkout local-branch'

            sh 'mv .env.example .env'
            // Cleanup actions, notifications, etc.
            // Archive test results, artifacts, etc.
            echo 'Pipeline finished'
        }
        failure {
            echo 'Pipeline failed'
        }
    }
}
