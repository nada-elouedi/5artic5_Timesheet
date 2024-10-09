pipeline {
    agent any

    environment {
        GITHUB_URL = 'https://github.com/nada-elouedi/5artic5_Timesheet.git'
        BRANCH_NAME = 'NadaElouedi5arctic5' // Change this if needed
        GITHUB_CREDENTIALS_ID = 'githubtoken' // The ID of your GitHub token stored in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    // Checkout the specified branch using credentials
                    withCredentials([string(credentialsId: GITHUB_CREDENTIALS_ID, variable: 'GITHUB_TOKEN')]) {
                        git branch: BRANCH_NAME, credentialsId: GITHUB_CREDENTIALS_ID, url: "https://${GITHUB_TOKEN}@${GITHUB_URL}"
                    }
                }
            }
        }

        stage('Check Last Commit') {
            steps {
                script {
                    def lastCommit = sh(script: 'git log -1 --pretty=format:"%H - %an, %ar : %s"', returnStdout: true).trim()
                    echo "Last Commit: ${lastCommit}"
                }
            }
        }

        stage('Build Spring Boot App') {
            steps {
                script {
                    // Run Maven commands
                    sh 'mvn clean'
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
