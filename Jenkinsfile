pipeline {
    agent any

    stages {

        stage('Checkout Validation') {
            steps {
                echo 'Repository checkout successful'
            }
        }

        stage('Build Vote Image') {
            steps {
                bat 'docker build -t voting-app:%BUILD_NUMBER% app\\vote'
            }
        }

        stage('Build Worker Image') {
            steps {
                bat 'docker build -t worker-app:%BUILD_NUMBER% app\\worker'
            }
        }

        stage('Build Result Image') {
            steps {
                bat 'docker build -t result-app:%BUILD_NUMBER% app\\result'
            }
        }

        stage('Verify Images') {
            steps {
                bat 'docker images'
            }
        }

        stage('Cluster Validation') {
            steps {
                withEnv(["KUBECONFIG=C:\\Users\\Rohit\\.kube\\config"]) {
                    bat 'kubectl get nodes'
                }
            }
        }
    }
}