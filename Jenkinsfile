
pipeline {
    agent { label 'Jenkins-Agent' }

    tools {
        jdk 'Java17'
        maven 'maven3'
    }

    stages {
        stage("Cleanup Workspace") {
            steps {
                cleanWs()
            }
        }
        
        stage("Checkout from SCM") {
            steps {
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/niroshaum/register-app'
            }
        }
        
        stage("Build Application") {
            steps {
                sh "mvn clean package"
            }
        }
        
        stage("Test Application") {
            steps {
                sh "mvn test"
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            cleanWs()  // Ensures workspace cleanup after the pipeline finishes
        }
        success {
            echo 'Build and tests were successful!'
        }
        failure {
            echo 'Build or tests failed.'
        }
    }
}
