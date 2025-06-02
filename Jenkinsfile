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
        stage('Checkov') {
            steps {
                withCredentials([string(credentialsId: 'PC_USER', variable: 'pc_user'),string(credentialsId: 'PC_PASSWORD', variable: 'pc_password')]) {
                    script {
                        docker.image('bridgecrew/checkov:latest').inside("--entrypoint=''") {
                            unstash 'source'
                            try {
                                sh 'checkov -d . --use-enforcement-rules -o cli -o junitxml --output-file-path console,results.xml --bc-api-key ${pc_user}::${pc_password} --repo-id  tomyawsmomi/jenkins-pipeline-demos --branch main'
                                junit skipPublishingChecks: true, testResults: 'results.xml'
                            } catch (err) {
                                junit skipPublishingChecks: true, testResults: 'results.xml'
                                throw err
                            }
                        }
                    }
                }
                options {
                    preserveStashes()
                    timestamps()
           }
         }
       }
    }
  }
