pipeline {
    agent any
    stages {
        stage('Clone Repo') {
            steps {
                    git branch: 'main', url: 'https://github.com/VickyTerm/My-DevOps-Portfolio.git'             }
        }
        stage('Deploy to S3') {
            steps {
                sh '''
                aws s3 sync . s3://dvignesh-portfolio \
                --exclude "*" \
                --include "*.html" \
                --delete
                '''
            }
        }
        stage('Invalidate CloudFront') {
            steps {
                sh '''
                aws cloudfront create-invalidation \
                --distribution-id E3S0PZQYR5XNK \
                --paths "/*"
                '''
            }
        }
    }
    post {
        success {
            echo '🚀 Portfolio deployed successfully!'
        }
        failure {
            echo '❌ Deployment failed. Check logs.'
        }
    }
}
