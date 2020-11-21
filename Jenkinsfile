pipeline {
    agent any 

    environment {
        PATH = "$PATH:/usr/local/bin"
    }

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
                sh label: '', script: '''docker-compose up -d --timeout=120
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
        stage('Push container') {
            steps {
                echo "Workspace is $WORKSPACE"
                dir("$WORKSPACE/azure-vote") {
                    script {
                        docker.withRegistry('https://index.docker.io/v1/', 'Jenkins') {
                            def image = docker.build('joelarnaud/jenkins-course.latest')
                            image.push()
                        }
                    }
                }
            }
        }
    }
}