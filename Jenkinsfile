pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Downloading source code from GitHub'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Preparing website files'

                sh '''
                    test -s index.html
                    echo "Website file found"
                '''
            }
        }

        stage('Test') {
            steps {
                echo 'Testing website'

                sh '''
                    grep -q "My First DevOps Project" index.html
                    grep -q "Website deployed through Jenkins" index.html
                    echo "Website tests passed"
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying website to Apache'

                sh '''
                    install -m 644 index.html \
                    /var/www/html/jenkins-demo/index.html
                '''
            }
        }

        stage('Verify') {
            steps {
                echo 'Verifying deployed website'

                sh '''
                    test -s /var/www/html/jenkins-demo/index.html

                    grep -q "Website deployed through Jenkins" \
                    /var/www/html/jenkins-demo/index.html

                    echo "Deployment verified"
                '''
            }
        }
    }

    post {
        success {
            echo 'SUCCESS: Website deployed to Apache!'
        }

        failure {
            echo 'FAILED: Check the Jenkins Console Output'
        }
    }
}
