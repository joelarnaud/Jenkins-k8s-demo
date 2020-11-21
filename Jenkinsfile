pipeline {
    agent any 

    stages {
        stage('Verify Branch') {
            steps {
                echo "$GIT_BRANCH"
            }
        }
        stage('Docker in Build') {
            steps{
                sh label: '', script: '''docker image ls -a
'''
                sh label: '', script: '''cd azure-vote; docker image ls -a; docker build -t jenkins-pipeline .; docker image ls -a; cd ..
'''
            } 
        }
        stage('Start test app') {
            steps {
                sh label: '', script: ''' # Start App line missing ! ./scripts/test_container.ps1
'''
            }
            post {
                success {
                    echo "App started successfully :)"
                }
                failure {
                    echo "App failed to start :("
                }
            }
        }
        stage('Run Tests') {
            steps {
                sh label: '', script: '''pytest ./tests/test_sample.py
'''
            }
        }
        stage('Stop test app') {
            steps {
                sh label: '', script: '''docker-compose down
'''
            }
        }
    }
}