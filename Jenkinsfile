pipeline {
    agent any 

    stages {
        stage('Verify Branch') {
            steps {
                echo "$GIT_BRANCH"
            }
        }
        stage('Docker Build') {
            steps{
                sh label: '', script: '''docker image ls -a
'''
                sh label: '', script: '''cd azure-vote 
'''
                sh label: '', script: '''docker image ls -a
'''
                sh label: '', script: '''docker build -t jenkins-pipeline .
'''
                sh label: '', script: '''docker image ls -a
'''
                sh label: '', script: '''cd ..
'''
            }
        }
    }
}