pipeline {
    agent any

    environment {
        // Fetch credentials stored in Jenkins with the ID 'jenkins_credentials'
        JENKINS_CREDENTIALS = credentials('jenkins_credentials')
    }

    stages {
        stage('Clone Repository') {
            steps {
                // Replace 'your-git-repo-url' with the actual URL of your Git repository
                git url: 'https://github.com/gaman5575/python-release.git', branch: 'main'
            }
        }

        stage('Run Python Script') {
            steps {
                // Set environment variables for the Python script and run it
                withEnv(["JENKINS_USER=${JENKINS_CREDENTIALS_USR}", "JENKINS_TOKEN=${JENKINS_CREDENTIALS_PSW}"]) {
                    sh 'python3 jenkins-trigger.py'
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
