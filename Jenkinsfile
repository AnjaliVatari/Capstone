pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                // Checkout code from the repository
                git branch: "${env.BRANCH_NAME}", url: 'https://github.com/hshar/website.git'
            }
        }
        stage('Build') {
            steps {
                script {
                    // Build and publish website on port 82 if commit is made to master branch
                    if (env.BRANCH_NAME == 'master') {
                        sh 'docker build -t website:latest .'
                        sh 'docker run -d -p 82:80 website:latest'
                    }
                    // Only build the product if commit is made to develop branch
                    else if (env.BRANCH_NAME == 'develop') {
                        sh 'docker build -t website:latest .'
                    }
                }
            }
        }
    }
}
