pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Repository checkout successful'
            }
        }

        stage('Environment Info') {
            steps {
                bat 'cd'
                bat 'dir'
            }
        }

        stage('Git Version') {
            steps {
                bat 'git --version'
            }
        }

        stage('Docker Version') {
            steps {
                bat 'docker --version'
            }
        }

        stage('Kubectl Version') {
            steps {
                bat 'kubectl version --client'
            }
        }
    }
}