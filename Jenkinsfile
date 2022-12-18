pipeline {
    agent any
  
    stages {
        stage('SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/amaljo/react-todo-app.git'
            }
        }
        stage('Install Deps') {
            steps {
                sh 'npm install'
            }
        }
        stage('Build') {
            steps {
                sh 'npm run build'
            }
            post {
                success {
                    fingerprint 'build/'
                }
            }
        }
        stage('Deploy to Apache2') {
            steps {
                sh 'cp -rv build* /var/www/html/'
            }
        }
        stage('Archive Artifacts') {
            steps {
                sh '''
                  zip -r archive.zip build/*
                '''
                archiveArtifacts artifacts: 'archive.zip', fingerprint: true, onlyIfSuccessful: true
            }
        }
    }
}