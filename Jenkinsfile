pipeline {
    agent any
    
    stages {
        stage('Clone') {
            steps {
                echo 'Cloning Repo...'
            }
        }
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
            }
        }
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/tomyawsmomi/jenkins-pipeline-demos.git'
                stash includes: '**/*', name: 'source'
            }
           }
         }
       }
