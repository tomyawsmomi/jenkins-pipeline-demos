pipeline {
    agent any

    environment {
        PRISMA_API_URL = "https://api.eu.prismacloud.io"
    }

    options {
        preserveStashes()
        timestamps()
    }

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
                withCredentials([
                    string(credentialsId: 'PC_USER', variable: 'pc_user'),
                    string(credentialsId: 'PC_PASSWORD', variable: 'pc_password')
                ]) {
                    script {
                        unstash 'source'
                        try {
                            sh '''
                                checkov -d . --use-enforcement-rules -o cli \
                                --bc-api-key ${pc_user}::${pc_password} \
                                --repo-id tomyawsmomi/jenkins-pipeline-demos --branch main
                            '''
                        } 
                    }
                }
            }
        }
    }
}
